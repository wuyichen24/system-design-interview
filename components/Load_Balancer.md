# Load Balancer (LB)

## Concepts
- Distribute incoming network traffic across a group of backend servers.

## Functionalities
### Main Functionalities
- Distribute client requests or network load efficiently across multiple healthy servers.

### Other Functionalities
| Function | Description |
|----|----|
| Asymmetric load | A ratio can be manually assigned to cause some backend servers to get a greater share of the workload than others. |
| TLS offload | Load balancer can terminate TLS connections, passing HTTPS requests as HTTP requests to the backend servers. |
| Health checking | Load balancer can check the health of the backend servers and remove unhealthy ones from the pool. |

## Layer Options
| | Layer 4 | Layer 7 |
|---|---|---|
| Layer | Transport layer | Application layer |
| Unit | Packet | Message |
| Decision | Not based on the content of the packet | Based on the content of the message |

## Types
- Hardware
- Software

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

## Cons
- Load balancer can be a potential performance bottleneck.
- A single load balancer is a single point of failure.
- Load balancer increases the system complexity.

## References
- https://www.nginx.com/resources/glossary/load-balancing/
