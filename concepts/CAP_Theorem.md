# CAP Theorem

## Concepts
- A distributed computer system can only support two of the following 3 guarantees:
   - Consistency: Every read receives the most recent write or an error.
   - Availability: Every request receives a (non-error) response, without the guarantee that it contains the most recent write.
   - Partition tolerance: The system continues to operate despite an arbitrary number of messages being dropped (or delayed) by the network between nodes.
