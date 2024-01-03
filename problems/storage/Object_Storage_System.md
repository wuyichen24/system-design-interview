# Object Storage System

- [**Real-life examples**](#real-life-examples)
- [**Requirements clarification**](#requirements-clarification)
- [**Estimation**](#estimation)
- [**System interface definition**](#system-interface-definition)
- [**Data model definition**](#data-model-definition)
- [**High-level design**](#high-level-design)
- [**Detailed design**](#detailed-design)
   - [Data store](#data-store)
      - [High-level design](#high-level-design-1)
      - [Data persistence flow](#data-persistence-flow)
      - [How data is organized](#how-data-is-organized)
   - [Metadata data model](#metadata-data-model)
   - [Object versioning](#object-versioning)
   - [Optimizing uploads of large files](#optimizing-uploads-of-large-files)
- [**Key points**](#key-points)
- [**References**](#references)
 
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
- **Download object**
   - `GET /bucket_name/object_name`

## Data model definition

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

#### How data is organized
- **Store many small objects into a larger file**:
   - When we save an object, it is appended to an existing read-write file.
   - When the read-write file reaches its capacity threshold, the read-write file is marked as read-only, and a new read-write file is created to receive new objects.
   - Once a file is marked as read-only, it can only serve read requests.

     <img width="500" alt="store-multiple-small-objects" src="https://github.com/wuyichen24/system-design-interview/assets/8989447/e3aed7fa-0eba-442f-840a-09856be3d9f0">

- **Use the `object_mapping` table to store the relationship between object and file**

  | Field | Description |
  |----|----|
  | object_id | UUID of the object |
  | file_name | The name of the file that contains the object. |
  | start_offset | Beginning address of the object in the file. |
  | object_size | The number of bytes in the object. |

  <img width="500" alt="updated-data-persistence" src="https://github.com/wuyichen24/system-design-interview/assets/8989447/f5d9284b-6533-4e0e-99b9-3d1b4d663a72">

### Metadata data model
- **Tables**
   - *objects*
     
     | Field | Description |
     |----|----|
     | object_name | The name of the object. |
     | object_id | The UUID of the object. |
     | bucket_id | Which bucket the object belongs to. |
     | object_version | The version number (TIMEUUID) of the object. |
  
   - *buckets*

     | Field | Description |
     |----|----|
     | bucket_name | The name of the bucket. |
     | bucket_id | The UUID of the bucket. |
     | owner_id | The owner of the bucket. |
     | enable_versioning | The bucket enabled versioning or not. |
     
- **Sharding key**
   - The hash of the combination of `bucket_name` and `object_name`.
    
### Object versioning
- **If an existing object is modified**
   - Insert a new record in the `objects` table.
      - Same `bucket_id` and `object_name` as the old record.
      - Generate new `object_id` (UUID) and `object_version` (TIMEUUID) for the new record.
      - The current version has the largest TIMEUUID of all the entries with the same object_name. 

  <img width="500" alt="versioned-metadata" src="https://github.com/wuyichen24/system-design-interview/assets/8989447/3be21f15-1d2d-4e7d-95f4-44d1765d3771">

### Optimizing uploads of large files
- **Solution**
   - Slice a large object into smaller parts and upload them independently.
   - After all the parts are uploaded, the object store re-assembles the object from the parts.

  <img width="300" alt="multipart-upload" src="https://github.com/wuyichen24/system-design-interview/assets/8989447/5b890dd7-a398-48ca-b068-759060610691">

## Key points
- The data store does not store the name of the object and it only supports object operations via object_id (UUID).
- Multiple small objects will be stored in a single file. Use the `object_mapping` table to locate the object in a certain file.
- Same data will be replicated to different data nodes, also replicated to different Availability Zones.
- For supporting multiple versions of an object, the `object_name` should be same but `object_id` (UUID) should be new.

## References
- [System Design Interview – An insider's guide | S3-like Object Storage](https://bytebytego.com/courses/system-design-interview/s3-like-object-storage)
