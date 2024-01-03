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

## High-level design
