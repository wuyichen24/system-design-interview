# system-design-interview

## Knowledage
For system design knowledge, please find [system-design-knowledge](https://github.com/wuyichen24/system-design-knowledge) repo.

## Interview
- [Procedure](interview/Procedure.md)

## Problems
### Feed System
| Problem | Examples |
|----|----|
| [Build Follower Feed System](problems/feed/Build_Follower_Feed_System.md) | <li>Twitter |
| [Build Friend Feed System](problems/feed/Build_Friend_Feed_System.md) | <li>Facebook |

### Location System
| Problem | Examples |
|----|----|
| [Build Proximity System](problems/Build_Proximity_System.md) | <li>Yelp |
| [Build Nearby Friends System](problems/Build_Nearby_Friends_System.md) | |

### Video processing system
| Problem | Examples |
|----|----|
| [Build Video Distribution System](problems/Build_Video_Distribution_System.md) | <li>Youtube<li>Netflix<li>Vimeo |

### Storage system
| Problem | Examples |
|----|----|
| [Build Cloud File Storage System](problems/Build_Cloud_File_Storage_System.md) | <li>Google Drive<li>Microsoft OneDrive<li>Dropbox |
| [Build Cloud Object Storage System]() | <li>AWS S3 |
| [Build Key-value Store]() | |

### Booking system
| Problem | Examples |
|----|----|
| [Build Hotel Reservation System](problems/Build_Hotel_Reservation_System.md) | <li>Airbnb<li>Priceline |
| [Build Ticket Selling System]() | <li>Ticketmaster |
 
### Other system
| Problem | Examples |
|----|----|
| [Build URL Shortening System](problems/Build_URL_Shortening_System.md) | <li>TinyUrl |
| [Build Messaging System](problems/Build_Messaging_System.md) | <li>Facebook Chat<li>Whatapp<li>Slack |
| [Build Photo Sharing System](problems/Build_Photo_Sharing_System.md) | <li>Instagram<li>Flickr<li>Picasa |
| [Build Typeahead/Autocomplete System](problems/Build_Typeahead_Autocomplete_System.md) | |
| [Build Payment System](problems/Build_Payment_System.md) | <li>Amazon |
| [Build Live Commenting System](problems/Build_Live_Commenting_System.md) | | 
| [Build Privacy Setting System](problems/Build_Privacy_Setting_System.md) | |
| [Build Recommendation System](problems/Build_Recommendation_System.md) | |
| [Build Search System](problems/Build_Search_System.md) | |
| [Build Rate Limiter](problems/Build_Rate_Limiter.md) | |
| [Build Flash Sale System](problems/Build_Flash_Sale_System.md) | |
| [Build Unique ID Generator](problems/Build_Unique_ID_Generator.md) | |
| [Build Auction System](problems/Build_Auction_System.md)* | eBay |
| [Build Stock Exchange System](problems/Build_Stock_Exchange_System.md) | Robinhood |

* = incomplete

### More topics will be added
- Build a key-value store (System design interview vol1)
- Build a web crawler (System design interview vol1)
   - Prioritize web pages that are dynamic as these pages appear  more frequenctly in search engine ranking
   - The crawler should not be unbounded on the same domain.
   - Build a system that constantly tracks new web pages
- Build a notification system (System design interview vol1)
- Build a map system - Google map (System design interview vol2)
- Build a distributed message queue (System design interview vol2)
- Build a metrics monitoring alerting system (System design interview vol2)
- Build a AD click event aggregation system (System design interview vol2)
- Build a distributed email system (System design interview vol2)
- Build a cloud object storage system (System design interview vol2)
- Build a real-time gaming leaderboardboard (System design interview vol2)
- Build a ticket selling system - ticketmaster
- Build a currency exchange system
- Build a flash sale system
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
