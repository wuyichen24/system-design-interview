# Cache

## Types
| Type | Description |
|----|----|
| Client caching | Caches can be located on the client side (OS or browser). |
| CDN caching | CDNs are considered a type of cache. |
| Web server caching | Reverse proxies and web server can cache request or content. |
| Database caching | Databases include some level of caching. |
| Application caching | Caches can be located between the application and the data storage. |

## Algorithms
| Algorithm | Description |
|----|----|
| Least recently used (LRU) | Discards the least recently used items first. | 
| First in first out (FIFO) | Like queue, the cache evicts the blocks in the order they were added, without any regard to how often or how many times they were accessed before. |
| Last In First Out (LIFO) | Like stack, the cache evicts the block added most recently first without any regard to how often or how many times it was accessed before. |
