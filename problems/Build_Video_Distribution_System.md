# Build Video Distribution System

## Real-life Examples
- Youtube
- Netflix
- Vimeo

## Requirements Clarification
- **Functional requirements**
   - Upload video: Users can upload videos.
   - Watch video: Users can watch videos.
   - Search video: Users can search videos.
   - Comment video: Users can leave comments to videos, also like or dislike.
- **Non-functional requirements**
   - High reliability (any video uploaded should not be lost).
   - High availability.
   - High consistency is desirable (It should be ok for a user doesn’t see a video for a while).

## High-level design

![Build_Video_Distribution_System](https://user-images.githubusercontent.com/8989447/117078614-6f59fc80-acf7-11eb-8f51-81e5baacd007.png)

- **Upload Service**
   - Handle upload requests
   - Create a encoding task and push it into the processing queue.
- **Processing Queue**
   - Store all the encoding tasks.
   - Decouple uploading works and encoding works
   - It can act as a buffer if the encoder is unavailable or overloaded.
- **Encoder**
   - Encode each uploaded video into multiple formats.
- **Thumbnails generator**
   - Generate a few thumbnails for each video.
- **Video Storage**
   - Store video contents.
- **Thumbnails Storage**
   - Store thumbnails.
- **Video Metadata Database**
   - Store all the information about videos like title, file path in the system, uploading user, total views, likes, dislikes, comments.
- **User Database**
   - Store user’s information.
