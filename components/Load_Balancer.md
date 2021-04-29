# Load Balancer (LB)

## Concepts
- Distribute incoming network traffic across a group of backend servers.

## Functionalities
- Distribute client requests or network load efficiently across multiple healthy servers.

## Types


## Algorithms
- Random
   - Requests are distributed randomly.
- Random with two choices
   - Picks two servers at random and then choose the better one.
- Round robin
   - Requests are distributed sequentially.
- Less work
   - Requests are distributed to the server with the fewest work.
- Hash
   - Requests are distributed according to a hash table.
