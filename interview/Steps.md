# Steps

## Step 1: Requirements Clarification
- Description
   - Ask questions about the exact scope of the problem.
   - Clarify what parts of the system we will be focusing on.
- Types of requirements
   - Functional requirements
      - General features to common applications
      - Special features to different applications  
   - Non-functional requirements
      - Consistency
      - Availability
      - Performance

## Step 2: Estimation
- Description
   - Estimate the scale of the system we’re going to design.
- Steps for estimation
   - Estimate the scale of application
      - (Daily) User size
      - (Daily) User's common action' frequency
   - Estimate the storage
      - Types (Database, file system)
      - Capacity
   - Estimate the bandwidth
      - Calculation: Bandwidth = Data size need to transfer per day / time of a day

## System interface definition
- Description
   - Define what APIs are expected from the system.
- Example
  ```
  executeAction1(param1_1, param1_2, param1_3)
  executeAction2(param2_1, param2_2, param2_3)
  executeAction2(param3_, param2_2, param2_3)
  ```
  ```
