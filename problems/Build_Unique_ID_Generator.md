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
- **Decentralized**: Each service generates generate ID respectively.
