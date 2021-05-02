# Procedure

## Step 1: Requirements Clarification
- Description
   - Ask questions about the exact scope of the problem.
   - Clarify what parts of the system we will be focusing on.
- Sub-steps
   - Step 1.1: Functional requirements
      - Read actions
      - Write actions
      - Other functional behaviors 
   - Step 1.2: Non-functional requirements
      - Consistency
      - Availability
      - Performance

## Step 2: Estimation
- Description
   - Estimate the scale of the system we’re going to design.
- Sub-steps
   - Step 2.1: Estimate traffic/usage
      - Identify the system is read-heavy or write-heavy.
      - Estimate read-write ratio (The ratio between read actions and write actions).
      - Estimate the times of read actions and write actions per month/day.
      - Estimate the frequencies of read actions and write actions per second (QPS).
   - Step 2.2: Estimate storage
      - Estimate the types of storages (Database, file system).
      - Estimate the capacity of storage
          - Use the times of write actions in a period to calculate the number of records will be created in the period.
          - Total capacity needed in the period = Number of records x Size of a record
   - Step 2.3: Estimate bandwidth
      - Write bandwidth = Frequency of writes per second x Size of one record
      - Read bandwidth = Frequency of reads per second x Size of one record

## Step 3: System interface definition
- Description
   - Define what APIs are expected from the system.
- Example
  ```
  executeAction1(param1_1, param1_2, param1_3)
  executeAction2(param2_1, param2_2, param2_3)
  executeAction2(param3_1, param3_2, param3_3)
  ```

## Step 4: Data model definition
- Description
   - Identify various entities and how they will interact with each other.
   - Find proper database systems and other storage we should use.
      - Database: SQL or NoSQL dtatbase.
      - Block storage: Store photos and videos.
- Aspects of data model
   - Entities (Which tables do we need?)
   - Entities' fields (Which columns do we need for each table?)
   - Entities' relationship (Is there any foreign key relationship between tables?)

## Step 5: High-level design
- Description
   - Draw a block diagram with 5-6 boxes representing the core components of our system.
- Common core components
   - Client/User
   - Load balancer
   - Application server
   - Database
   - File storage

## Step 6: Detailed Design
- Description
   - Dig deeper into two or three major components.
   - Provide different options, their pros and cons, and explain why we will prefer one approach over the other.

## Step 7: Identify and solve bottlelnecks
- Description
   - Identify potential bottlenecks
   - Provide solutions for the bottlenecks
- Common bottlenecks
   - Performance bottleneck
   - Single point of failure
