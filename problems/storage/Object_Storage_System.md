# Object Storage System

## Real-life examples
- AWS S3

## Requirements clarification
- **Functional requirements**
   - Bucket creation: Users can create buckets.
   - Object uploading and downloading: Users can upload or download objects to/from buckets.
   - Object versioning: One object can have multiple versions.
   - Listing objects in a bucket: User can see all object information of a bucket.
- **Non-functional requirements**
   - High availability
   - Storage efficiency (Reduce storage costs while maintaining a high degree of reliability and performance).
 
## Estimation

## System interface definition
- **Upload object**
   - `PUT /bucket_name/object_name`
- **Download**
   - `GET /bucket_name/object_name`

## Data model definition
- **Entry for metadata**
   - Schema
       - object_name: The name of the object (file name).
       - object_id: UUID of the object.
       - bucket_id: UUID represents which bucket the object belongs to.
   - Example
     | object_name | object_id | bucket_id|
     |----|----|----|
     | script.txt | 239D5866-0052-00F6-014E-C914E61ED42B | 82AA1B2E-F599-4590-B5E4-1F51AAE5F7E4 |

## High-level design
![object_storage](https://github.com/wuyichen24/system-design-interview/assets/8989447/aa9b3f35-8244-4ae7-94bd-b949ed60b34e)

- **Load balancer**
   - Distributes RESTful API requests across a number of API servers.
- **API service**
   - Orchestrates remote procedure calls to the identity and access management service, metadata service, and storage stores.
- **Identity and access management (IAM)**
   - Handles authentication, authorization, and access control.
- **Metadata store**
   - Stores the metadata of the objects.
- **Data store**
   - Stores and retrieves the actual data.

## Detailed design
### Data store
#### High-level design

<img width="600" alt="data_store" src="https://github.com/wuyichen24/system-design-interview/assets/8989447/c0d1988a-14ac-43c0-98a5-97bdb52f26cd">

- **Data Routing Service**
   - Provides RESTful or gRPC APIs to access the data node cluster.
   - Queries the placement service to get the best data node to store data.
   - Reads data from data nodes and return it to the API service.
   - Writes data to data nodes.
- **Placement Service**
   - Determines which data nodes (primary and replicas) should be chosen to store an object.
   - Maintains a virtual cluster map, which provides the physical topology of the cluster.
   - Continuously monitors all data nodes through heartbeats.
 
     <img width="600" alt="virtual-cluster-map" src="https://github.com/wuyichen24/system-design-interview/assets/8989447/6f6db642-11c6-4c93-911b-ee3dc964e6be">
     
- **Data node**
   - Stores the actual object data.
   - Ensures reliability and durability by replicating data to multiple data nodes, also called a replication group.

#### Data persistence flow
<img width="600" alt="data-persistence" src="https://github.com/wuyichen24/system-design-interview/assets/8989447/3936fa60-2e41-4ea4-b330-4a7811ae2a84">

- *Step 1*: The API service forwards the object data to the data store.
- *Step 2*: The data routing service generates a UUID for this object and queries the placement service for the data node to store this object. The placement service checks the virtual cluster map and returns the primary data node.
- *Step 3*: The data routing service sends data directly to the primary data node, together with its UUID.
- *Step 4*: The primary data node saves the data locally and replicates it to two secondary data nodes. The primary node responds to the data routing service when data is successfully replicated to all secondary nodes.
- *Step 5*: The UUID of the object (ObjId) is returned to the API service.
