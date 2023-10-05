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

- **Matching engine**
   - Maintains the order book (the list of buy and sell orders) for each symbol.
   - Matches buy and sell orders. A match results in two executions (fills), with one each for the buy and sell sides.
   - Distributes the execution stream as market data.
- **Sequencer**
   - Stamps every incoming order with a sequence ID before it is processed by the matching engine (Inbound).
   - Stamps every pair of executions (fills) completed by the matching engine with sequence IDs (Outbound).
  
  <img width="504" alt="Screenshot 2023-10-04 at 8 48 28 PM" src="https://github.com/wuyichen24/system-design-interview/assets/8989447/6e34f5e4-6676-4af3-8648-7ec3649b20b8">
