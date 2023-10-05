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
   - Read-heavy.

## Data model definition
  
## High-level design
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

## Detailed Design
![Screen Shot 2021-05-26 at 2 03 54 AM](https://user-images.githubusercontent.com/8989447/119624692-a4251500-bdc6-11eb-8df9-05a8096caad6.png)
