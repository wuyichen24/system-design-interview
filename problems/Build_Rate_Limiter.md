# Build Rate Limiter

## Real-life examples

## Requirements clarification
- **Functional requirements**
   - Limit requests: Limit the number of requests an entity can send to an API within a time window.
   - Exception handling: The user should get an error message when the user excess the threshold.
   - Distribution: The rate limiter can monitor requests among multiple servers.
- **Non-functional requirements**
   - High availability (The rate limiter should always work for protecting the servers from external attacks).
   - Low latency (The rate limiter should not introduce substantial latencies affecting the user experience).

## Detailed design
### Algorithms for rate limiting
- **Token bucket**
   - Mechanism
      - The bucket can hold at the most B tokens.
      - A token is added to the bucket every R seconds. If the bucket is full, no more tokens are added.
      - When a reuqest arrives
         - If there is a token in the bucket, the request will take one token out from the bucket and it goes through.
         - If there is no token in the bucket, the request will be blocked.
        
           ![token_bucket drawio](https://user-images.githubusercontent.com/8989447/155385390-aa3f9b9f-e1f7-4472-9601-8a520ad60676.png)
   - Implementation details
      - Based on rate-limiting rules, we may need multiple buckets:
         - If we need to throttle request based on IP addresses/users. so each IP address/user requires a bucket.
         - If we need to throttle request based on request types (make a post, get feeds, etc.), so each request type requires a bucket.
   - Pros
      - Easy to implement.
      - Memory effcient.
   - Cons
      - Hard to tune the bucket size (B) and the refill rate (R) properly.
- **Leaking bucket**
   - Mechanism
      - A FIFO queue works as a bucket and it can hold at the most N requests.
      - The FIFO queue pops out (leak) a request at a fixed rate and let it be processed.
      - When a request arrives
         - If the queue is not full, the request will be added to the queue.
         - If the queue is full, the request will be blocked.

           ![leaky_bucket drawio](https://user-images.githubusercontent.com/8989447/155578782-e668a61f-cc47-40ad-8fc9-5e6599192047.png)
   - Pros
      - Memory effcient.
   - Cons
      - Recent requests will be blocked and only old requests will be processed when the queue is full.
      - Token bucket can send large bursts at a faster rate while leaky bucket always sends requests at constant rate.
- **Fixed window counter**
   - Mechanism
      - Divide the timeline to a fixed time window and assign a counter to each window.
      - When a request arrives
         - If the counter of the current time window doesn't reach the threshold, increment the counter by one and the request goes through.
         - If the counter of the current time window reached the threshold, the request will be blocked.
         
           ![fixed_time_window drawio](https://user-images.githubusercontent.com/8989447/155586579-bcb77111-f072-4d55-856f-9ad4515f4a6f.png)
   - Pros
      - Easy to implement.
      - Memory effcient.
   - Cons
      - A traffic spike at the edges of a window could cause more requests than the allowed quota to go through.

        ![fixed_time_window drawio (1)](https://user-images.githubusercontent.com/8989447/155587144-0dc77e8a-f3cd-4e73-9cc7-4b792446cfb2.png)
- **Sliding window log**
   - Mechanism
      - Use timestamp logs to track every request's timestamp. 
      - When a request arrives
         - Only focus on the logs are in the current time window (From now to the start of the current time window) and ignore the logs are not in the current time window.
         - Count how many logs are in the current time window
            - If the number doesn't reach the threshold, the request will go through.
            - If the number reaches the threshold, the request will be blocked.

              ![sliding-window-log](https://user-images.githubusercontent.com/8989447/155608074-e690722b-922d-4819-9996-bc39bc08303a.png)
   - Pros
      - Avoid the drawback of the fixed window counter algorithm.
   - Cons
      - Memory inefficient (For each request, have to filter logs and count the number of logs)
- **Sliding window counter**
   - Concepts
      - The sliding window counter is the combination of the fixed window counter and the sliding window log.
      - The basic idea of sliding window counter is to add a weighted count in previous time period to the count in current period.
   - Mechanism
      - Given the limiting rate is N requests per minute. 
      - For current sliding window, there are overlaps on both the current minute and the previous minute. The overlap on the previous minute is P%.
      - There were A requests received in the previous minute and there were B requests received in the current minute.
      - So the number of requests in the current sliding window will be B + P% * A.
      - Compare the number of requests in the current sliding window with threshold
         - If the number doesn't reach the threshold (B + P% * A < N), the request will go through.
         - If the number reaches the threshold (B + P% * A ≥ N), the request will be blocked.
   - Pros
      - Memory effcient.

## References
- https://medium.com/swlh/rate-limiting-fdf15bfe84ab
- https://hechao.li/2018/06/25/Rate-Limiter-Part1/
