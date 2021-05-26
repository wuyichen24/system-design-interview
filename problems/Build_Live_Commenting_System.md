# Build Live Commenting System

## Requirements clarification
- **Functional requirements**
   - Write: Users can write real-time comments to posts.
   - Read: Users can read real-time comments from posts.

## High-level design
- There are 2 ways to publish comments to users
   - Push (Fanout and write): Maintains a connection with user to directly send new comments directly.
      - Pros
         - Easy to implement
      - Cons
         - User cannot get the comments generated when he was offline.
         - For mobile platform, system resources are limited to handle lots of new comment.
   - Pull (Fanout and load): User needs to request the server to get the new comments when required.
      - Pros
         - User can get the comments generated when he was offline.
      - Cons
         - System have to handle a larget amount of requests.
      
![Screen Shot 2021-05-26 at 1 51 43 AM](https://user-images.githubusercontent.com/8989447/119623063-0aa93380-bdc5-11eb-8b45-f46f8d28aa02.png)

## Detailed Design
![Screen Shot 2021-05-26 at 1 54 02 AM](https://user-images.githubusercontent.com/8989447/119623336-4d6b0b80-bdc5-11eb-88dd-c172d01fe557.png)
