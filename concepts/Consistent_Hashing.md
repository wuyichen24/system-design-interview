# Consistent Hashing

## Concepts
- A special hashing technique that when a hash table is resized, only k/n keys need to be remapped on average.
   - k is the total number of keys.
   - n is the total number of servers.
   
## Algorithm
- **Basic**
   - Create a new ring based on the range of hashing [0, h]
      - The starting point is 0 (12 o'clock's direction).
      - The ending point is h (right next to the starting point).
   - Evenly place the servers to the ring.
     
     ![ch1](https://user-images.githubusercontent.com/8989447/117730978-8c387900-b1aa-11eb-8bd5-6eaedbc0be04.png)  ![ch2](https://user-images.githubusercontent.com/8989447/117731167-ea655c00-b1aa-11eb-9d61-f101e951ab7b.png)
   
- **Map a key to a server**
   - Get the hash value of the key: hash(key).
   - hash(key) will be represented a position on the ring.
   - The key will assigned to the next server that appears on the circle in clockwise order from the position. 
   - If the assigned server is failed:
      - The key will be be reassigned to the next server in clockwise order.

     ![ch3](https://user-images.githubusercontent.com/8989447/117731784-f1409e80-b1ab-11eb-8d64-ecd141276d57.png)  ![ch4](https://user-images.githubusercontent.com/8989447/117732075-70ce6d80-b1ac-11eb-9349-f148aed9872b.png)

## Benefits
- Minimize reorganization/rebalance when servers are added or removed.
