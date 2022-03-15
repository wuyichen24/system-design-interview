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
  ![uniqueID drawio](https://user-images.githubusercontent.com/8989447/158303619-8472b8a4-74b0-4da7-9132-de96b1a89a30.png)
- **Decentralized**: Each service generates generate ID respectively.
