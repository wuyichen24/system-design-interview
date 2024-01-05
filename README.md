# system-design-interview

## Knowledage
For system design knowledge, please find [system-design-knowledge](https://github.com/wuyichen24/system-design-knowledge) repo.

## Interview
- [Procedure](interview/Procedure.md)

## Problems
### Social Media System
| Problem | Examples |
|----|----|
| [Follower Feed System](problems/social_media/Follower_Feed_System.md) | <li>Twitter |
| [Friend Feed System](problems/social_media/Friend_Feed_System.md) | <li>Facebook |
| [Messaging System](problems/social_media/Messaging_System.md) | <li>Facebook Chat<li>Whatapp<li>Slack |
| [Photo Sharing System](problems/social_media/Photo_Sharing_System.md) | <li>Instagram<li>Flickr<li>Picasa |
| [Privacy Setting System](problems/social_media/Privacy_Setting_System.md) | |

### Location System
| Problem | Examples |
|----|----|
| [Proximity System](problems/location/Proximity_System.md) | <li>Yelp |
| [Nearby Friends System](problems/location/Nearby_Friends_System.md) | |
| Map system (System design interview vol2) | Google map |

### Video processing system
| Problem | Examples |
|----|----|
| [Video Distribution System](problems/video/Video_Distribution_System.md) | <li>Youtube<li>Netflix<li>Vimeo |

### Storage system
| Problem | Examples |
|----|----|
| [File Storage System](problems/storage/File_Storage_System.md) | <li>Google Drive<li>Microsoft OneDrive<li>Dropbox |
| [Object Storage System](problems/storage/Object_Storage_System.md) **Done** | <li>AWS S3 |
| [Key-value Store]()* | |
| Distributed message queue (System design interview vol2) | |

### Booking system
| Problem | Examples |
|----|----|
| [Hotel Reservation System](problems/booking/Hotel_Reservation_System.md) | <li>Airbnb<li>Priceline |
| [Ticket Selling System]()* | <li>Ticketmaster |

### Finance system
| Problem | Examples |
|----|----|
| [Payment System](problems/finance/Payment_System.md) | |
| [Stock Exchange System](problems/finance/Stock_Exchange_System.md) | Robinhood |

### Support system
| Problem | Examples |
|----|----|
| [Rate Limiter](problems/support/Rate_Limiter.md) | |
| [Unique ID Generator](problems/support/Unique_ID_Generator.md) | |
| [Notification System](problems/support/Notification_System.md) | |
| [Web Crawler](problems/support/Web_Crawler.md) **Done** | |
| [Search System](problems/support/Search_System.md) | |
| [Typeahead/Autocomplete System](problems/support/Typeahead_Autocomplete_System.md) | |
| [URL Shortening System](problems/support/URL_Shortening_System.md) | <li>TinyUrl |
| [Metrics Monitoring and Alerting System](problems/support/Metrics_Monitoring_And_Alerting_System.md) **Done** | <li>Datadog<li>New Relic<li>Prometheus<li>Graphite |

- distributed email system (System design interview vol2)

### Other system
| Problem | Examples |
|----|----|
| [Ad Click Event Aggregation System](problems/Ad_Click_Event_Aggregation_System.md) **Done** | |
| [Live Commenting System](problems/Live_Commenting_System.md) | | 
| [Recommendation System](problems/Recommendation_System.md) | |
| [Flash Sale System](problems/Flash_Sale_System.md) | |
| [Auction System](problems/Auction_System.md)* | eBay |

`*` = incomplete

### More topics will be added
- Build a real-time gaming leaderboardboard (System design interview vol2)
- Build a currency exchange system
- Build a traffic control system
  - Requirements
     - A group of traffic lights has two components: main lights and pedestrian lights.
     - Main traffic lights have three colors: red, yellow and green.
     - Pedestrian lights have two colors: red and green.
     - Pedestrian lights' colors are reversed from main lights:
        - Main: red/yellow - pedestrian's: green
        - Main: green - pedestrian: red
     - There is a button for pedestrian lights if the button is pushed in advance, pedestrian's lights change colors according to the main ones if the button isn't pushed, pedestrian's lights remain red.
     - A typical junction has 4 groups of lights.
     - Additional question: design the system in a way that allows cars which start from one junction after a red light don't have to stop at the next one.
  - Key points in solution
     - Cnosider all phase transitions (from red to green, red to orange to green, and so on)
     - Be clear on the conditions in which a certain transition will take place
     - Consider pedestrian crossing requirements
     - Determine cycle length
     - Determine clearance time
     - Apportion green light approriately
- Build a counter system for online services
- Build a game of chess
- Build a parking garage
- Build an online bookstore
- Build an e-commerce website
   - How to handle transactions?
- Build an elevator system
- Build a vending machine
- Build a task management system - Trello
   - Requirement
      - User can move tasks from one lane to the other and move it back.
      - This should have a state diagram with many end states.
- Build a card game
   - There should be more than one method of cards distribution such as even distribution, uneven distribution, etc.
   - There are multiple situations which could be considered as a winning situation:
      - One who finishes all his cards early.
      - One who earns the maximum points at the last.
- Build a restaurant management system.

## More problems
- https://tianpan.co/notes/2016-02-13-crack-the-system-design-interview
- https://medium.com/coders-mojo/complete-system-design-series-part-1-45bf9c8654bc

## Education platform comparison
[Exponent](https://www.tryexponent.com/courses/system-design-interview?ref=techinterviewhandbook)
- Design a URL Shortener
- Design Instagram
- Design Amazon Prime Video
- Design YouTube
- Design TikTok
- Design Uber Eats
- Design Facebook Messenger
- Design ChatGPT
- Design a Parking Garage
- Design a Rate Limiter
- Design the Payment System for the Amazon Kindle
- Design a Landmark Recognition System
- Design Typeahead for Search Box
- Design a Hotel Booking Service
- Design a Web Crawler
- Design a Distributed Message Queue

[Design Gurus | Grokking Modern System Design Interview](https://www.designgurus.io/course/grokking-the-system-design-interview?aff=kJSIoU)
- Designing a URL Shortening Service like TinyURL
- Designing Pastebin
- Designing Instagram
- Designing Dropbox
- Designing Facebook Messenger
- Designing Twitter
- Designing Youtube or Netflix
- Designing Typeahead Suggestion
- Designing an API Rate Limiter
- Designing Twitter Search
- Designing a Web Crawler
- Designing Facebook’s Newsfeed
- Designing Yelp or Nearby Friends
- Designing Uber backend
- Designing Ticketmaster

[Educative | Grokking Modern System Design Interview for Engineers & Managers](https://www.educative.io/courses/grokking-modern-system-design-interview-for-engineers-managers)
- Design YouTube
- Design Quora
- Design Google Maps
- Design a Proximity Service / Yelp
- Design Uber
- Design Twitter
- Design Newsfeed System
- Design Instagram
- Design a URL Shortening Service / TinyURL
- Design a Web Crawler
- Design WhatsApp
- Design Typeahead Suggestion
- Design a Collaborative Document Editing Service / Google Docs

## Presentation
| Topic | Source 1 | Source 2 |
|----|----|----|
| Scaling Instagram Infrastructure | [InfoQ](https://www.infoq.com/presentations/instagram-scale-infrastructure/) | [Youtube](https://www.youtube.com/watch?v=hnpzNAPiC0E) |
| How Slack Works | [InfoQ](https://www.infoq.com/presentations/slack-infrastructure/) | [Youtube](https://www.youtube.com/watch?v=WE9c9AZe-DY) |
| Scaling Slack - The Good, the Unexpected, and the Road Ahead | [InfoQ](https://www.infoq.com/presentations/slack-scalability-2018/) | [Youtube](https://www.youtube.com/watch?v=_M-oHxknfnI) |
| Scaling Slack | [InfoQ](https://www.infoq.com/presentations/slack-scalability/) | [Youtube](https://www.youtube.com/watch?v=x1Uz3rMlOBo) |
| Twitter: Timelines at Scale | [InfoQ](https://www.infoq.com/presentations/Twitter-Timeline-Scalability/) | |
| How We Learned to Stop Worrying and Love Fan-In at Twitter | | [Youtube](https://www.youtube.com/watch?v=WEgCjwyXvwc) |
| Scaling Pinterest | | [Youtube](https://www.youtube.com/watch?v=jQNCuD_hxdQ) |
| Scaling Redis at Twitter | | [Youtube](https://www.youtube.com/watch?v=rP9EKvWt0zo) |
| Systems at Facebook Scale | | [Youtube](https://www.youtube.com/watch?v=dlixGkelP9U) |
| Building Real Time Infrastructure at Facebook | | [Youtube](https://www.youtube.com/watch?v=ODkEWsO5I30) |
| Lessons of Scale at Facebook | | [Youtube](https://www.youtube.com/watch?v=QCHiNEw73AU) |
| The Evolution of Reddit.com's Architecture | | [Youtube](https://www.youtube.com/watch?v=nUcO7n4hek4) |
| Scalable and Reliable Logging at Pinterest | | [Youtube](https://www.youtube.com/watch?v=DphnpWVYeG8) | 
| Facebook and memcached | | [Youtube](https://www.youtube.com/watch?v=UH7wkvcf0ys) |

## References
- https://leetcode.com/discuss/interview-question/3766958/Bookmark-It-%3A-System-Design-and-Most-popular-Coding-Questions
