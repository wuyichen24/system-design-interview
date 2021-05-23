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
      - Estimate the total number of users and daily active users (DAU)
         - USER_NUM.
      - Estimate the number of read actions and write actions per user per month/week/day
         - ACTION_NUM_PER_USER.
      - Estimate the total number of read actions and write actions for the system per month/week/day.
         - ACTION_NUM_PER_SYSTEM = USER_NUM X ACTION_NUM_PER_USER
      - Estimate the frequencies of read actions and write actions per second (QPS).
         - QPS = ACTION_NUM_PER_SYSTEM / TIME
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
- Recommendations
   - If an interface is for registered accounts only, add `api_key` as a parameter.

## Step 4: Data model definition
- Description
   - Identify tables and how they will interact with each other.
- Sub-steps
   - Step 4.1: Build the schema.
      - Tables
      - Columns and column type
      - Foreign key relationship between tables
   - Step 4.2: Choose a proper database and other storage.
      - Database: SQL or NoSQL dtatbase.
      - Object storage: Store photos and videos.

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
