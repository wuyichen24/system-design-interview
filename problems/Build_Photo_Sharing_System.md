# Build Photo Sharing System

## Real-life Examples
- Instagram
- Flickr
- Picasa

## Requirements Clarification
- **Functional requirements**
   - Upload: Users can upload photos.
   - View: Users can view photos.
   - Search: Users can search photos.
   - Follow: Users can follow other users.
   - News feed: Users can see the top/new photos from the users they follow.
- **Non-functional requirements**
   - High availability
   - High reliability (any photo uploaded should not be lost).
   - High consistency is desirable (It should be ok for a user doesn’t see a photo for a while).
   - Low latency is expected while viewing photos.

## Estimation
- **Traffic estimation**
   - Our system will be read-heavy.
   - Users
      - 500 million users. (Assumed)
      - 1 million daily active users. (Assumed)
   - Photos
      - 2 million new photos every day (Assumed)
      - Average photo file size = 200 KB (Assumed)
- **Storage estimation**
   - Types
      - Data: Yes
      - File: Yes
   - Capacity
      - Total capacity needed every day = Number of new photos every day x Average photo file size = 2 million x 200 KB =  400 GB
- **Bandwidth estimation**

## System interface definition

## Data model definition

## High-level design
