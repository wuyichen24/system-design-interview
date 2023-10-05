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

## Detailed Design
- **Solutions**
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


