# Build Privacy Setting System

## Requirements clarification
- **Functional requirements**
   - Set privacy level: Users can specify the different levels of privacy for a post so that it is only visible to a particular set of users.
   - Read privacy level: Feed generation service will make lots of requests to check privacy level of users for new posts.
- **Non-functional requirements**
   - Low latency.
   - High consistency (Same privacy setting should be applied to all the devices).
   - High availability is desirable (base on CAP theorem).

## Estimation
- **Traffic estimation**
   - Our system will be read-heavy.

## High-level design
- Use Enum data type to define the different privacy levels:
   - Public
   - Friends
   - Friends of friends
   - Custom
   - Private
- Each post will have a privacy level field.
- Store the user relationship data in a key-value store (cache).
   - Key = UserID, Value = A set of all the friends.
   - Sharded across multiple instances.
- Friends of friends
   - Perform an intersection of the post's owner and the viewer's friend lists.
   - Add a record of friend of friend (A-B, B-C, so add A-C into the user relationship data).

![Screen Shot 2021-05-26 at 2 14 13 AM](https://user-images.githubusercontent.com/8989447/119626119-1d713780-bdc8-11eb-99d3-39b9cd39790b.png)
![Screen Shot 2021-05-26 at 2 16 00 AM](https://user-images.githubusercontent.com/8989447/119626341-54dfe400-bdc8-11eb-996a-0b1cb576be1e.png)
![Screen Shot 2021-05-26 at 2 16 48 AM](https://user-images.githubusercontent.com/8989447/119626473-7e007480-bdc8-11eb-8bc6-ab0954808024.png)


