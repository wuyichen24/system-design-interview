# Build Search System

## High-level design
![Screen Shot 2021-05-26 at 1 47 31 AM](https://user-images.githubusercontent.com/8989447/119622411-5ad3c600-bdc4-11eb-81a5-bfaba3df4fc0.png)

## Detailed Design
![Screen Shot 2021-05-26 at 1 45 47 AM](https://user-images.githubusercontent.com/8989447/119622163-252edd00-bdc4-11eb-8586-ff23e7307c92.png)
![Screen Shot 2021-05-26 at 11 00 20 AM](https://user-images.githubusercontent.com/8989447/119701475-9c3e9280-be11-11eb-839d-8ad229b2643b.png)

## Detailed Design
- What if an index server dies?
   - Have a secondary replica of each server and if the primary server dies it can take control after the failover.
   - Rebuild index
      - Iiterate through the whole database
      - Build a reverse index that will map all the TweetID to their index server.
         - Our Index-Builder server can hold this information.
         - Key = index server number. Value = HashSet containing all the TweetIDs being kept at that index server.
