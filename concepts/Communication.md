# Communication

## OSI Model
| Number | Name | Protocol Data Unit | Decription | Common Protocols |
|----|----|----|----|----|
| 7 | Application | Data | High-level APIs. | HTTP (HTTP/1, HTTP/2), HTTPS, RPC, SOAP, WebSocket, FTP, SFTP, SMTP, LDAP, SSH, DHCP, DNS  |
| 6 | Presentation | Data | Translation of data between a networking service and an application. | |
| 5 | Session | Data | Managing communication sessions. | |
| 4 | Transport | Segment, Datagram | Reliable transmission of data segments between points on a network. | TCP, UDP, TLS/SSL |
| 3 | Network | Packet | Structuring and managing a multi-node network. | IP (IPv4, IPv6) |
| 2 | Data Link | Frame | Reliable transmission of data frames between two nodes connected by a physical layer. | |
| 1 | Physical | Bit, Symbol | Transmission and reception of raw bit streams over a physical medium. | |

## Common Protocols
| Name | Layer | Features |
|----|----|----|
| UDP | Transport layer (L4) | <li>Connectionless<li>Unreliable |
| TCP | Transport layer (L4) | <li>Connection-based<li>Reliable |
| HTTP | Application layer (L7) | |
  
## Common Mechanisms
### REST
- **Pros**
   - Simple
   - Easy to debug (You can debug by web browsers, Postman and curl command)
   - Firewall-friendly (Can be used for public APIs).
   - Stateless.
- **Cons**
   - Only supports request-response style.

### RPC
- **Concepts**
   - Allows a computer program to cause a procedure to execute in another address space (commonly on another computer on a shared network).
- **Frameworks**
   - Google gRPC
   - Facebook Thrift
   - Apache Avro
- Pros
   - Efficient for exchanging large data.
   - Bidirectional streaming.
- Cons
   - Hard to debug.
   - Not flexible.
   - Old firewalls don’t support HTTP/2-based RPCs (Cannot be used for public APIs).
  
### WebSocket
