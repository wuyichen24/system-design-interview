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
- **Decentralized**: Each server generates ID respectively.
   - Pros
      - Improve availability.
   - Cons
  
  ![uniqueID drawio (1)](https://user-images.githubusercontent.com/8989447/158303949-72981c78-a56f-460f-b024-d1d9f039e6e8.png)

## Detailed design
### Solution options for centralized architecture
- **Zookeeper**
   - Concept
      - Distributed coordinator to give each server a unique unused range of IDs.
        
        ![Untitled Diagram drawio (2)](https://user-images.githubusercontent.com/8989447/158518927-2d831af3-c5fa-412f-9af8-5304561bd561.png)
   - Pros
      - Easy to implement.
   - Cons
      - IDs cannot be ordered by time cross multiple servers.
      - Need to consider the size of each range.

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
      - IDs cannot be ordered by time.
- **Snowflake ID**
   - Concepts
      - The format was created by Twitter and is used for the IDs of tweets.
      - Divide an ID into different sections:
         - Sign (1 bit): Always be 0 (Reserved for future used).
         - Timestamp (41 bits): Milliseconds since the epoch or custom epoch.
         - Machine ID (10 bits): Hold up to 1024 machines.
         - Sequence number (12 bits): The sequence number is incremented by 1 and is reset to 0 every millisecond.
      -  64-bit.
      - Each machine can generate IDs by itself.

        <img width="709" alt="Snowflake-identifier" src="https://user-images.githubusercontent.com/8989447/158496043-0a8c6bf4-b991-47da-adb4-d884014d0054.png">
   - Pros
     - IDs can be ordered by time.
     - The binary representation of the timestamp field can be converted to/from a a real date and time.
   - Cons
