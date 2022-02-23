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
- Leaking bucket
- Fixed window counter
- Sliding window log
- Sliding window counter
