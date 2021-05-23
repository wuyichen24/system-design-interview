# Cache

## Types

![Cache](https://user-images.githubusercontent.com/8989447/118215761-6cfe4d80-b42f-11eb-9ac2-2e43553b36f1.png)

### Client-side caching
| Type | Description |
|----|----|
| Browser caching | Web browsers on the client side can cache some web content. |
| App caching | Applications (mobile or PC) on the client side can cache some content. |

### Server-side caching
| Type | Description | Examples |
|----|----|----|
| CDN caching | CDNs can cache some static resources (web page, media file, etc.). | |
| Reverse proxy caching | Reverse proxy server can cache responses to clients. | | 
| In-Process caching | An object cache built within the same memory as the application. | <li>Ehcache<li>Caffine<li>Google Guava Cache |
| Database caching | Databases include some level of caching. | |
| Application caching | Caches can be located between the application and the data storage. | <li>Redis<li>Memcached<li>Tair |

## Replacement Policies
| Algorithm | Description |
|----|----|
| Least recently used (LRU) | Discards the least recently used items first. | 
| Most recently used (MRU) | Discards the most recently used items first. |
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

## Common Problems And Solutions
| Problem | Scenario | Cause | Solutions |
|---|---|---|---|
| Cache avalanche | Lots of cached data expire at the same time or the cache instance is down. | Suddenly all queries hit the database and cause the database to crash down. | <li>Use distributed cache cluster (Redis cluster) to achieve high availability.<li>Use Hystrix's circuit breaker and rate limit to avoid the database crash down by high load.<li>Use the combination of in-process cache and distributed cache.<li>Adjust the expiration time for different keys so that they will not expire at the same time. |
| Cache penetration | Lots of queries for the data which doesn't exist in the database. | For those queries, database doesn't have the data and cache doesn't have too. But those queries will eventually the hit the database. If the amount of the queries is very large, it would cause the database to crash down. | <li>Let the cache still store the null result for the query (with short expiration time).<li>Use Bloom filter to filter out some queries which cannot have data in the database at all. |
| Cache breakdown | A very hot data entry expires in the cache. | Suddenly lots of queries for that that very hot data entry will hit the database eventually and cause the database to crash down. | <li>Add a lock on that data entry and the lock only allows a very limited amount of queries to search the data entry from the database and update the cache. After releasing the lock, other queries can get that data entry from the cache directly.<li>Asynchronously update that data entry from database so that the data entry will never expire.<li>Don't set the expiration time on that data entry if it will never be changed. |

## Related Concepts
- **Distributed Cache**
   - A distributed cache may span multiple servers so that it can grow in size and in transactional capacity.
- **Cache Coherence**
   - The uniformity of shared resource data that is stored in multiple local caches.
   - If one client updates the memory block, another client could be left with an invalid cache of memory without any notification of the change.

     <img width="304" alt="Cache_Coherency_Generic" src="https://user-images.githubusercontent.com/8989447/118202935-310bbe00-b418-11eb-9fbb-547fe155e05b.png">
- **Cold Cache, Warm Cache and Cache Warming**
   - Cold Cache: The cache has no data in it and cannot provide cache hits.
   - Warm Cache: The cache has data it it can can provide cache hits.
   - Cache Warming: Manually pre-fill a cold cache with data so that it can provide cache hits when receiving real requests.
   - Cache Warmer: The tools for warning caches.
      - Examples: Magento, Wordpress.
   
## References
- https://docs.microsoft.com/en-us/azure/architecture/best-practices/caching
- https://www.pixelstech.net/article/1586522853-What-is-cache-penetration-cache-breakdown-and-cache-avalanche
- https://github.com/doocs/advanced-java/blob/main/docs/high-concurrency/redis-caching-avalanche-and-caching-penetration.md
- https://github.com/dunwu/blog/blob/master/source/_posts/theory/cache.md
