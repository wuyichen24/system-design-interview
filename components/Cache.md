# Cache

## Types
| Type | Description |
|----|----|
| Client caching | Caches can be located on the client side (OS or browser). |
| CDN caching | CDNs are considered a type of cache. |
| Web server caching | Reverse proxies and web server can cache request or content. |
| Database caching | Databases include some level of caching. |
| Application caching | Caches can be located between the application and the data storage. |

## Algorithms (Replacement)
| Algorithm | Description |
|----|----|
| Least recently used (LRU) | Discards the least recently used items first. | 
| | Most recently used (MRU) | Discards the most recently used items first. |
| First in first out (FIFO) | Like queue, the cache evicts the blocks in the order they were added, without any regard to how often or how many times they were accessed before. |
| Last in first out (LIFO) | Like stack, the cache evicts the block added most recently first without any regard to how often or how many times it was accessed before. |
| Random replacement (RR) | Randomly selects a candidate item and discards it to make space when necessary. |
| Least-frequently used (LFU) | Discards the least often used items first. |

## Strategies
- [**Cache-Aside**](https://github.com/wuyichen24/distributed-system-design-pattern/blob/master/patterns/cache_patterns/Cache_Aside.md)
- [**Cache-As-SOR**](https://github.com/wuyichen24/distributed-system-design-pattern/blob/master/patterns/cache_patterns/Cache_As_Sor.md)
   - Read-Through
   - Write-Through
   - Write-Behind
   - Refresh-Ahead
