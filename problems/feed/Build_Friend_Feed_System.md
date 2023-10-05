# Build Friend Feed System

## Real-life examples
- Facebook

## Requirements clarification
- **Functional requirements**
   - A user can publish a post.
   - A user can see friends' post on the feed page.
   - A post can contain media files, including both images and videos.
- **Non-functional requirements**

## High-level design

![feed](https://github.com/wuyichen24/system-design-interview/assets/8989447/b13499d4-6c60-4a62-9681-749da4e2eb2e)

- **Web servers**
   - Enforces authentication and rate-limiting.
- **Fanout service**
   - Delivers a post to all friends
      - Fetch friend IDs from the graph database and get friends info from the user cache.
      - Send friends list and new post ID to the message queue.
- **Fanout workers**
   - Fetches data from the message queue and store news feed data in the news feed cache.
   - Inserts `<post_id, user_id>` into news feed cache.
- **Graph DB**
   - Manages friend relationship and friend recommendations.
- **News Feed Cache**
   - Stores `<post_id, user_id>`
