# URL Shortening Service

## Requirements Clarification
- **Functional requirements**
   - URL Shortening (Write): Given an original URL, our service should generate a shorter and unique URL of it.
   - URL Redirection (Read): When users access a short URL, our service should redirect them to the original URL.
   - URL Customization: Users should optionally be able to pick a custom short URL for their original URL.
   - URL Expiration: Shorter URL will expire after a standard default timespan. Users should be able to specify the expiration time.
- **Non-functional requirements**
   - The system should be highly available (ff our service is down, all the URL redirections will start failing).
   - URL redirection should happen in real-time with minimal latency.
   - Shortened links should not be guessable (not predictable).

## Estimation
- **Traffic estimation**
   - Our system will be read-heavy (Lots of redirection requests compared to new URL shortenings).
   - Read-write ratio is 100 : 1 (*Assumed*)
   - Number of read actions and write actions per month
      - Number of writes (URL Shortening) per month = 500 millions (*Assumed*)
      - Number of reads (URL Redirection) per month= 500 millions x 100 = 50 billion
   - Frequency of read actions and write actions per second (QPS)
      - Frequency of writes per second = 500 millions / (30 days x 24 hours x 3600 seconds) = 200 times/s 
      - Frequency of reads per second = 200 times/s x 100 = 20000 times/s
- **Storage estimation**
   - Types
      - Data: Yes
      - File: No
   - Capacity
      - Time length of storing a record = 5 years (*Assumed*)
      - Number of records created in 5 years = Number of writes per month x Number of months = 500 million x 5 years x 12 months = 30 billion
      - Size of one record = 500 bytes (*Assumed*)
      - Total capacity needed in 5 years = 30 billion * 500 bytes = 15 TB
- **Bandwidth estimation**
   - 
