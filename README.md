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
| [Cloud File Storage System](problems/storage/Cloud_File_Storage_System.md) | <li>Google Drive<li>Microsoft OneDrive<li>Dropbox |
| [Cloud Object Storage System]()* | <li>AWS S3 |
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

### Tool system
| Problem | Examples |
|----|----|
| [Rate Limiter](problems/Build_Rate_Limiter.md) | |
| [Unique ID Generator](problems/Build_Unique_ID_Generator.md) | |
| [Build Notification System](Build_Notification_System.md) | |

- metrics monitoring alerting system (System design interview vol2)
- AD click event aggregation system (System design interview vol2)
- distributed email system (System design interview vol2)
- web crawler (System design interview vol1)
   - Prioritize web pages that are dynamic as these pages appear  more frequenctly in search engine ranking
   - The crawler should not be unbounded on the same domain.
   - Build a system that constantly tracks new web pages

### Other system
| Problem | Examples |
|----|----|
| [URL Shortening System](problems/Build_URL_Shortening_System.md) | <li>TinyUrl |
| [Typeahead/Autocomplete System](problems/Build_Typeahead_Autocomplete_System.md) | |
| [Live Commenting System](problems/Build_Live_Commenting_System.md) | | 
| [Privacy Setting System](problems/Build_Privacy_Setting_System.md) | |
| [Recommendation System](problems/Build_Recommendation_System.md) | |
| [Search System](problems/Build_Search_System.md) | |
| [Flash Sale System](problems/Build_Flash_Sale_System.md) | |
| [Auction System](problems/Build_Auction_System.md)* | eBay |


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
