# Consistent Hashing

## Concepts
- A special hashing technique that when a hash table is resized, only k/n keys need to be remapped on average.
   - k is the total number of keys.
   - n is the total number of servers.
   
## Algorithm
- Create a new ring based on the range of hashing [0, h]
   - The starting point is 0 (12 o'clock's direction).
   - The ending point is h (right next to the starting point).
- Evenly place the servers to the ring.
- Map a key to a server:
   - Get the hash value of the key: hash(key).
   - hash(key) will be represented a position on the ring.
   - The key will assigned to the next server that appears on the circle in clockwise order from the position. 
- If the assigned server is failed:
   - The key will be be reassigned to the next server in clockwise order.
