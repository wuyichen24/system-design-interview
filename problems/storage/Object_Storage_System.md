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
