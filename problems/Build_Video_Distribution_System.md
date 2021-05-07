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

## Estimation
- **Traffic estimation**
   - Our system will be read-heavy.
   - Read-write ratio (View-upload ratio) is 200 : 1 (Assumed)
   - Users
      - 1.5 billion users. (Assumed)
      - 150 million daily active users. (Assumed)
      - 1% of users are creators, every week will publish one new video. (Assumed)
      - Each user watches 3 videos per day. (Assumed)
   - Number of read actions and write actions per week
      - Number of writes (upload) per week = 1.5 billion x 1% = 15 million
      - Number of reads (watch) per week = 15 millions x 200 = 3 billion
   - Frequency of read actions and write actions per second (QPS)
      - Frequency of writes per second = 15 millions / (7 days x 24 hours x 3600 seconds) = 24 videos/s
      - Frequency of reads per second = 24 videos/s x 200 = 4800 videos/s
- **Storage estimation**
   - Types
      - Data: Yes
      - File: Yes
   - Capacity
      - Size of each video: 500 MB (Assumed)
      - Total capacity needed in week = Number of writes (upload) per week x Size of one record = 15 million x 500 MB = 7152 TB
- **Bandwidth estimation**
   - Size of each video: 500 MB (Assumed)
   - Write bandwidth = Frequency of writes per second x Size of one record = 24 videos/s x 500 MB = 11 GB/s
   - Read bandwidth = Frequency of reads per second x Size of one record = 4800 videos/s x 6 MB/s (1080p) = 28 GB/s

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
