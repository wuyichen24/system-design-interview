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

## Types
- **Hardware vs. Software**
  | | Hardware | Software |
  |----|----|----|
  | Rely on | Proprietary hardware | Commodity hardware |
  | Pros | | <ul><li>Low cost<li>High agility</ul> |
 
- **Layer 4 vs. Layer 7**
  | | Layer 4 | Layer 7 |
  |---|---|---|
  | Layer | Transport layer | Application layer |
  | Unit | Packet | Message |
  | Decision | <ul><li>**Not based on the content of the packet.**<li>Based on the source, destination IP addresses and ports recorded in the packet header.</ul> | <ul><li>**Based on the content of the message.**<ul><li>HTTP header<li>URL<li>The type of data (text, video, graphics)<li>Information in a cookie</ul></ul> |
  | Pros | <ul><li>Simple<li>Better performance<li>Better granularity</ul>| <ul><li>Can make smarter load‑balancing decisions<li>Can apply optimizations and changes to the content (such as compression and encryption).<li>Can use buffering to offload slow connections from the upstream servers (Improve performance).</ul> |

## Algorithms
| Name | Description | Pros | Cons |
|----|----|----|----|
| Random | Requests are distributed randomly. | | |
| Random with two choices | Picks two servers at random and then choose the better one. | | |
| Round robin | Requests are distributed sequentially. | | |
| Least connections | Requests are distributed to the server with the fewest active connections to clients. | | |
| Least time | Requests are distributed to the server with the combination of lowest response time and fewest active connections. | | |
| Least work/load | Requests are distributed to the server with the fewest work. | | |
| Hash | Requests are distributed according to a hash table you define. | | |
| IP hash | Requests are distributed based on the IP address of the client. | | |

## Cons
- Load balancer can be a potential performance bottleneck.
- A single load balancer is a single point of failure.
- Load balancer increases the system complexity.

## Redundant Load Balancers
- Concepts
   - To remove the load balancer as a single point of failure, a second load balancer can be connected to the first to form a cluster.
- Operations
   - Each load balancer monitors the health of the other.
   - In the event the primary load balancer fails, the secondary load balancer takes over.
   
   ![ha-diagram-animated](https://user-images.githubusercontent.com/8989447/118159733-a2c51700-b3da-11eb-8501-33cec29c11f6.gif)

## Related Concepts
- **Session Persistence**
   - All requests from a client are sent to the same server for the duration of the session.
- **Dynamic Configuration of Server Groups (Autoscaling)**
   - The load balancer can dynamically add or remove servers from the server group without interrupting existing connections.
- **Cloud Load Balancing**
   - Distributing client requests across multiple application servers that are running in a cloud environment.
- **Hybrid Load Balancing**
   - Distributing client requests across a set of server applications that are running in various environments: on premises, in a private cloud, and in the public cloud.
- **DNS Load Balancing**
   - Configuring a domain in the Domain Name System (DNS) such that client requests to the domain are distributed across a group of server machines.
- **SSL Load Balancer**
   - A load balancer that also performs encryption and decryption of data transported via HTTPS, which uses the Secure Sockets Layer (SSL) protocol (or its successor, the Transport Layer Security (TLS) protocol) to secure HTTP data as it crosses the network.

## References
- https://www.nginx.com/resources/glossary/load-balancing/
