# Build Recommendation System

## Requirements clarification
- **Functional requirements**
   - Get the top N trending topics for a user over the past X days.
   - The popularity of a topic can be determined by the frequency of the topic being viewed in the past.
- **Non-functional requirements**
   - Low latency.
   - High availability.
   - High consistency is desirable (eventual consistency).

## Detailed Design
- Track topics
   - Log the view history into application service
   - A background async process with read the data from these logs, do some initial aggregation.
- 2 Solutions for generating top N trending topics
   - Fast path
      - A data structure called Count-Min Sketch will be used.
      - Take short time but less accurate.
   - Slow path
      - MapReduce pipeline
      - Take long time but more accurate.

## High-level design
![Screen Shot 2021-05-26 at 2 07 23 AM](https://user-images.githubusercontent.com/8989447/119625157-20b7f380-bdc7-11eb-823a-96f03105f4e1.png)
![Screen Shot 2021-05-26 at 2 08 06 AM](https://user-images.githubusercontent.com/8989447/119625245-3a593b00-bdc7-11eb-9737-edb6023cfce8.png)
![Screen Shot 2021-05-26 at 2 08 56 AM](https://user-images.githubusercontent.com/8989447/119625374-59f06380-bdc7-11eb-93e0-bd29a3408b54.png)
