# Build Unique ID Generator

## Requirements clarification
- **Functional requirements**
   - Mandatory requirements
      - ID must be unique among the whole distributed system.
   - Optional requirements
      - IDs can be ordered by time.
- **Non-functional requirements**
   - The generator should be highly available.
   - ID generation should happen in real-time with minimal latency.
   
## High-level design
### Architecture options
- **Centralized**: Use one centralized service to generate ID.
   - Pros
      - Easy to implement.
   - Cons
      - Introduce single point of failure.

  ![uniqueID drawio](https://user-images.githubusercontent.com/8989447/158303619-8472b8a4-74b0-4da7-9132-de96b1a89a30.png)
- **Decentralized**: Each service generates ID respectively.
   - Pros
      - Improve availability.
   - Cons
  
  ![uniqueID drawio (1)](https://user-images.githubusercontent.com/8989447/158303949-72981c78-a56f-460f-b024-d1d9f039e6e8.png)

## Detailed design
### Solution options for centralized architecture
### Solution optinos for decentralized architecture
- **UUID**
   - Concepts
      - UUID consists of 32 hexadecimal (base-16) digits, displayed in five groups separated by hyphens.
        ```
        123e4567-e89b-12d3-a456-426614174000
        ```
      - 128-bit.
   - Pros
      - Very low probability of getting collusion.
      - The ID generators in the services don't need to coordinate each other.
   - Cons
      - ID cannot be ordered by time.
- **Twitter snowflake**
   - Concepts
      - Divide an ID into different sections:
         - Sign (1 bit): Always be 0 (Reserved for future used).
         - Timestamp (41 bits): Milliseconds since the epoch or custom epoch.
         - Datacenter ID (5 bits): 32 available data centers (2<sup>5</sup>)
         - Machine ID (5 bits)
         - Sequence number (12 bits)
