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
- Token bucket
- Leaking bucket
- Fixed window
- Sliding window
