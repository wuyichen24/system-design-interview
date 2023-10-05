# Build Stock Exchange System

## Real-life examples

## Requirements clarification
- **Functional requirements**
   - User can place and cancel orders.
   - User can view the real-time order book (the list of buy and sell orders).
   - Only support trading stock.
- **Non-functional requirements**
   - *High availability*
      - Availability is crucial for exchanges
   - *Fault tolerance*
      - Fault tolerance and a fast recovery mechanism are needed to limit the impact of a production incident.
   - *Low latency*
      - The round-trip latency should be at the millisecond level.
   - *High security*
      - Verify a user’s identity before a new account is opened.
      - Prevent web pages from distributed denial-of-service (DDoS) attacks.
    
## High-level design

![stock_exchange](https://github.com/wuyichen24/system-design-interview/assets/8989447/3d6255e0-8c56-47d5-9d21-830b4af18d5f)
