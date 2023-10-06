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
   - Concept
      - Draw a circle with the predefined radius and find all the businesses within the circle.
      - Use the similar query:
        ```sql
        SELECT business_id, latitude, longitude,
        FROM business
        WHERE (latitude BETWEEN {:my_lat} - radius AND {:my_lat} + radius) AND
            (longitude BETWEEN {:my_long} - radius AND {:my_long} + radius)
        ```
   - Cons
      - The query is not efficient because we need to scan the whole table.
- **Evenly divided grid**
   - Concepts
      - Evenly divide the world into small grids
   - Cons
      - The distribution of businesses is not even (New York city vs. deserts).
- **Geohash**
   - Concepts
      - Reduce the two-dimensional longitude and latitude data into a one-dimensional string of letters and digits.
      - Recursively Divide the world into smaller and smaller grids with each additional bit.
      - The longer a shared prefix is between two geohashes, the closer they are.

        ![figure-9-shared-prefix-K37LAGTS](https://github.com/wuyichen24/system-design-interview/assets/8989447/6e2fbe1a-4422-47ce-8bac-177c6f4fb3e8)

   - Cons
      - Have boundary issues:
         - Two locations can be very close but have no shared prefix at all.

           ![figure-10-no-shared-prefix-MFLTKKDZ](https://github.com/wuyichen24/system-design-interview/assets/8989447/0d81854e-032c-4b84-bd4f-cc93cd1e6867)

         - Two locations can have a long shared prefix, but they belong to different geohashes.

           ![figure-11-boundary-issue-XJWRE2EX](https://github.com/wuyichen24/system-design-interview/assets/8989447/2a96dc01-08c2-46df-acc7-7cae180bbc6a)

- **Quadtree**
- **Google S2**
   - SQL
      - Select * from Places where Latitude between X-D and X+D and Longitude between Y-D and Y+D
      - Not efficient
         - Need to use range to query 2 columns.
   - Grids (Static size grid)
      - Divide the whole map into smaller grids to group locations into smaller sets.
      - Select * from Places where Latitude between X-D and X+D and Longitude between Y-D and Y+D and GridID in (GridID, GridID1, GridID2, ..., GridID8)
      - It could be a problem there are a lot of places in a single grid.
   - QuadTree (Dynamic size grids)
      - Structure
         - Each node has four children.
         - If a node reaches our limit of 500 places, we will break it down to create four child nodes under it.
         - Leaf nodes represents the grids that cannot be further broken down.
         - Root node represents the whole world in one grid.
      - Traversal
         - If the current node has children, move to the child node that contains our desired location and repeat this process.
      - Find neighboring grids
         - Connect all leaf nodes with a doubly linked list.
         - Through parent nodes (each node has a pointer to access its parent).


