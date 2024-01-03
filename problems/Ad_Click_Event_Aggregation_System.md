# Ad Click Event Aggregation System

## Real-life examples

## Requirements clarification
- **Context**
   - The input data is a log file located in different servers and the latest click events are appended to the end of the log file.
   - The attributes of input data are:
      - `ad_id`
      - `click_timestamp`
      - `user_id`
      - `ip`
      - `country`
- **Functional requirements**
   - Support 2 queries:
      - Aggregate the number of clicks of `ad_id` in the last `M` minutes.
      - Return the top 100 most clicked `ad_id` every minute.
   - For above queries, support aggregation filtering by different attributes (e.g. `ip`, `user_id`, etc.).
- **Non-functional requirements**
   - Correctness of the aggregation result is important.
   - Properly handle delayed or duplicate events.
   - Robustness. The system should be resilient to partial failures.
   - End-to-end latency should be a few minutes, at most.

## Estimation

## System interface definition
- **Aggregate the number of clicks of `ad_id` in the last `M` minutes**
   - URL: `GET /v1/ads/{:ad_id}/aggregated_count`
   - Request

     | Field | Description | Type |
     |----|----|----|
     | from | Start minute (default is now minus 1 minute) | long |
     | to | End minute (default is now) | long |
     | filter	| An identifier for different filtering strategies. (For example, filter = 001 filters out non-US clicks) | long |

   - Response

     | Field | Description | Type |
     |----|----|----|
     | ad_id | The identifier of the ad | string |
     | count | The aggregated count between the start and end minutes | long |
     
- **Return top `N` most clicked `ad_ids` in the last `M` minutes**
   - URL: `GET /v1/ads/popular_ads`
   - Request

     | Field | Description | Type |
     |----|----|----|
     | count | Top N most clicked ads | integer |
     | window | The aggregation window size (M) in minutes | integer |
     | filter | An identifier for different filtering strategies | long |

   - Response
 
     | Field | Description | Type |
     |----|----|----|
     | ad_ids | A list of the most clicked ads | array |

## Data model definition
- **Raw data**

     | ad_id | click_timestamp | user | ip | country |
     |----|----|----|----|----|
     | ad001 | 2021-01-01 00:00:01 | user1 | 207.148.22.22 | USA |
     | ad001 | 2021-01-01 00:00:02 | user1 | 207.148.22.22 | USA |
     | ad002 | 2021-01-01 00:00:02 | user2 | 209.153.56.11 | USA |
  
- **Aggregated data**
   - aggregated_result table

     | ad_id | click_minute | filter_id | count |
     |----|----|----|----|
     | ad001 | 202101010000 | 0012 | 2 |
     | ad001 | 202101010000 | 0023 | 3 |
     | ad001 | 202101010001 | 0012 | 1 |
     | ad001 | 202101010001 | 0023 | 6 |
     
   - filter table
  
     | filter_id | region | IP | user_id |
     |----|----|----|----|
     | 0012 | US | * | * |
     | 0013 | * | 123.1.2.3 | * |
     
   - most_clicked_ads table
 
     | Field | Type | Description |
     |----|----|----|
     | window_size | integer | The aggregation window size (M) in minutes. | 
     | update_time_minute | timestamp | Last updated timestamp (in 1-minute granularity) |
     | most_clicked_ads	| array | List of ad IDs in JSON format. |

- **Solution**
   - Store both raw data and aggregated data
      - The use cases of raw data
         - Debugging.
         - Recalculate the aggregated data from the raw data, after a bug fix.
         - Serve as backup data.
      - The use cases of aggregated data
         - Run queries on aggregated data for better performance.
 
## High-level design
<img width="800" alt="high-level" src="https://github.com/wuyichen24/system-design-interview/assets/8989447/73d0057a-0b7c-4717-88f5-384e101f81d1">

- **Log Watcher**
   - Reads log and publish ad click event data into the left message queue.
- **Message Queue (Left)**
   - Stores ad click event data.
- **Message Queue (Right)**
   - Stores
       - Ad click counts aggregated at per-minute granularity.
       - Top N most clicked ads aggregated at per-minute granularity.
   - Achieves end-to-end exactly-once semantics (atomic commit).
- **Data Aggregation Service**
   - Processes raw data and generate aggregated data.
- **Recalculation Service**
   - Recalculate the raw data and generate new aggregated data when we discover a major bug.
- **Reconciliation**
   - Sort the ad click events by event time in every partition at the end of the day, by using a batch job and reconciling with the real-time aggregation result.

## Detailed design
### Data Aggregation Service
- **Idea**
   - Use MapReduce framework
   - Break down the system into Map/Aggregate/Reduce nodes.
 
     <img width="600" alt="aggregation-service" src="https://github.com/wuyichen24/system-design-interview/assets/8989447/02d22150-60b0-40ef-9822-1b3b4c8d353e">
     
- **Components**
   - *Map node*
      - Reads data from a data source, and then filters and transforms the data.
   - *Aggregate node*
      - Counts ad click events by ad_id in memory every minute.
   - *Reduce node*
      - Reduces aggregated results from all “Aggregate” nodes to the final result.

- **Use cases**
   - *Case 1: Aggregate the number of clicks*
      - Input events are partitioned by ad_id (ad_id % 3) in Map nodes and are then aggregated by Aggregation nodes.
    
        <img width="800" alt="aggregate-the-number-of-clicks" src="https://github.com/wuyichen24/system-design-interview/assets/8989447/7e085260-0a91-4cb2-9df2-176f215f89f8">
        
   - *Case 2: Return top N most clicked ads*
      - Input events are partitioned by ad_id (ad_id % 3) in Map nodes.
      - Each Aggregate node maintains a heap data structure to get the top 3 ads within the node efficiently.
      - The Reduce node reduces 9 ads (top 3 from each aggregate node) to the top 3 most clicked ads every minute.

        <img width="800" alt="return-top-n-most-clicked-ads" src="https://github.com/wuyichen24/system-design-interview/assets/8989447/819076e0-59d5-4a29-8116-d7a63c56efcb">
        
   - *Case 3: data filtering*
      - Pre-define filtering criteria and aggregate based on them

### Aggregation window
- **Type of windows**
   - Tumbling window: Has a fixed length, and every event belongs to exactly one window.
   - Hopping window: Has a fixed length, but allows windows to overlap in order to provide some smoothing.
   - Sliding window: Contains all the events that occur within some interval of each other.
   - Session window: Has no fixed duration. Group together all events for the same user that occur closely together in time, and the window ends when the user has been inactive for some time.
- **Which window should be used for our use cases**
   - *Case 1: Aggregate the number of clicks*
      - Use Tumbling window

        ![figure-15-tumbling-window-2JXIXGIH](https://github.com/wuyichen24/system-design-interview/assets/8989447/46266b7b-f4e7-4963-b627-1cb464f92a5a)

   - *Case 2: Return top N most clicked ads*
      - Use sliding window

        ![figure-16-sliding-window-OTVSYTQA](https://github.com/wuyichen24/system-design-interview/assets/8989447/b35152df-4d28-4b75-a839-e226d4bdc4fc)


## Key points
- Store both raw data and aggregated data, raw data for debugging and backup, aggregated data for fast queries.
- Data aggregation service uses MapReduce framework and break down the problem into Map/Aggregate/Reduce nodes.
- Need to recalculate the raw data and generate new aggregated data when we discover a major bug.
- Should use event time rather than processing time.
