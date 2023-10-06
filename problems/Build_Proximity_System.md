# Build Proximity System

## Real-life examples
- Yelp

## Requirements clarification
- **Functional requirements**
   - A user can search businesses by the search radius.
   - Business owners can add, delete or update a business.
   - A user can view detailed information about a business.
- **Non-functional requirements**
   - *Low latency*
      - Users should be able to see nearby businesses quickly.
   - *High availability and scalability*
      - Our system can handle the spike in traffic during peak hours in densely populated areas.

## Estimation
- **Traffic estimation**
   - Read-heavy

## Data model definition
  
## High-level design

![figure-2-high-level-design-OLWE4F2G](https://github.com/wuyichen24/system-design-interview/assets/8989447/d8fd9d92-69b9-4417-b5f6-be9caebe6594)

![figure-21-design-diagram-ORKTOGMW](https://github.com/wuyichen24/system-design-interview/assets/8989447/6de1b8a5-4ba5-459d-b506-03918cdf3287)

- **Load balancer**
   - Distributes incoming traffic across multiple services.
- **Location-based service (LBS)**
   - Finds nearby businesses for a given radius and location.
   - Characteristics:
      - It is a read-heavy service with no write requests.
      - QPS is high, especially during peak hours in dense areas.
      - This service is stateless so it’s easy to scale horizontally.
- **Business service**
   - Allows business owners to create, update, or delete businesses.
   - Allows users to view detailed information about a business.
- **Database cluster**
   - Uses the primary-secondary setup.
      - The primary database handles all the write operations
      - The multiple replicas are used for read operations.

## Detailed Design
### Algorithms to fetch nearby businesses
- **Two-dimensional search**
   - *Concept*
      - Draw a circle with the predefined radius and find all the businesses within the circle.
      - Use the similar query:
        ```sql
        SELECT business_id, latitude, longitude,
        FROM business
        WHERE (latitude BETWEEN {:my_lat} - radius AND {:my_lat} + radius) AND
            (longitude BETWEEN {:my_long} - radius AND {:my_long} + radius)
        ```
   - *Cons*
      - The query is not efficient because we need to scan the whole table.
- **Evenly divided grid**
   - *Concepts*
      - Evenly divide the world into small grids
   - *Cons*
      - The distribution of businesses is not even (New York city vs. deserts).
- **Geohash**
   - *Concepts*
      - Reduce the two-dimensional longitude and latitude data into a one-dimensional string of letters and digits.
      - Recursively Divide the world into smaller and smaller grids with each additional bit.
      - The longer a shared prefix is between two geohashes, the closer they are.

        ![figure-9-shared-prefix-K37LAGTS](https://github.com/wuyichen24/system-design-interview/assets/8989447/6e2fbe1a-4422-47ce-8bac-177c6f4fb3e8)

   - *Cons*
      - Have boundary issues:
         - Two locations can be very close but have no shared prefix at all.

           ![figure-10-no-shared-prefix-MFLTKKDZ](https://github.com/wuyichen24/system-design-interview/assets/8989447/0d81854e-032c-4b84-bd4f-cc93cd1e6867)

         - Two locations can have a long shared prefix, but they belong to different geohashes.

           ![figure-11-boundary-issue-XJWRE2EX](https://github.com/wuyichen24/system-design-interview/assets/8989447/2a96dc01-08c2-46df-acc7-7cae180bbc6a)

- **Quadtree**
   - *Concepts*
      - Partition a two-dimensional space by recursively subdividing it into four quadrants (grids) until the contents of the grids meet certain criteria.
      - Quadtree is an in-memory data structure and it is not a database solution.

        ![figure-13-quadtree-MWKA5XCK](https://github.com/wuyichen24/system-design-interview/assets/8989447/0156d8da-2642-43d2-aa52-27c11c8c83fd)
        ![figure-14-build-quadtree-ZV3JS35E](https://github.com/wuyichen24/system-design-interview/assets/8989447/3a5f0387-d6bc-4d46-a684-2043bd625465)

        
- **Google S2**
   - *Concepts*
      - Map a sphere to a 1D index based on the Hilbert curve (a space-filling curve)
         - Two points that are close to each other on the Hilbert curve are close in 1D.
         - Search on 1D space is much more efficient than on 2D. 
      - Google S2 is an in-memory solution.
   - *Pros*
      - S2 is great for geofencing because it can cover arbitrary areas with varying levels (A geofence is a virtual perimeter for a real-world geographic area).
      - Region Cover algorithm
         - Instead of having a fixed level (precision) as in geohash, we can specify min level, max level, and max cells in S2.
         - The result returned by S2 is more granular because the cell sizes are flexible.
