# Build Nearby Friends System

## Real-life examples

## Requirements clarification
- **Functional requirements**
   - Users should be able to see nearby friends on their mobile apps.
   - Nearby friend lists should be updated every few seconds.
- **Non-functional requirements**
   - *Low latency*
      - Receive location updates from friends without too much delay.
   - *Moderate reliability*
      - Occasional data point loss is acceptable.
   - *Eventual consistency*
      - A few seconds delay in receiving location data in different replicas is acceptable.

## High-level design

![figure-5-restful-api-request-flow-SL4EZ27Z](https://github.com/wuyichen24/system-design-interview/assets/8989447/859eed81-4511-4221-b3ee-37b43cce2c4e)

- **Load Balancer**
   - Distributes traffic across those servers to spread out load evenly.
- **API Servers**
   - Handles auxiliary requests like adding/removing friends, updating user profiles.
- **WebSocket Servers**
   - Handles the near real-time update of friends’ locations.
   - Handles client initialization for the “nearby friends” feature.
- **Redis Pub/Sub**
   - A very lightweight message bus.
   - Location updates received via the WebSocket server are published to the user’s own channel in the Redis pub/sub server.
- **Location Cache**
   - Stores the most recent location data for each active user.
   - Sets a Time to Live (TTL) on each entry in the cache.
- **Location History Database**
   - Stores users’ historical location data (not directly related to the “nearby friends” feature).   
- **User Database**
   - Stores user data and user friendship data.
