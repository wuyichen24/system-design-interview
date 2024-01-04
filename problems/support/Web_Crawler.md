# Web Crawler

## Requirements clarification
- **Functional requirements**
   - Given a set of URLs, download all the web pages addressed by the URLs.
   - Track newly added or edited web pages.
   - Prioritize web pages that are dynamic as these pages appear more frequenctly in search engine ranking.
- **Non-functional requirements**
   - *High scalability*
      - Web crawling should be extremely efficient using parallelization.
   - *Robustness*
      - The crawler must handle all edge cases, like bad HTML, unresponsive servers, crashes, malicious links, etc.
   - *Politeness*
      - The crawler should not make too many requests to a website within a short time interval.
   - *Extensibility*
      - The system is flexible so that minimal changes are needed to support new content types (images, videos).

## High-level design

<img width="800" alt="Screenshot 2023-10-23 at 10 20 59 PM" src="https://github.com/wuyichen24/system-design-interview/assets/8989447/4cdd99dc-ccfa-43dd-a836-4cf1e4f05304">

- **Seed URLs**
   - A web crawler uses seed URLs as a starting point for the crawl process.
   - The general strategy is to divide the entire URL space into smaller ones.
      - Based on locality
      - Based on topics
- **URL Frontier**
   - Stores URLs need to be downloaded.
   - A First-in-First-out (FIFO) queue.
- **HTML Downloader**
   - Downloads web pages from the internet.
- **DNS Resolver**
   - The HTML Downloader calls the DNS Resolver to get the corresponding IP address for the URL.
- **Content Parser**
   - Parses and validate the content of web pages.
- **Content Seen?**
   - Detects new content previously stored in the system.
   - Eliminates data redundancy and shorten processing time.
   - To compare two two web pages, it compares the hash values of them.
- **Content Storage**
   - Stores HTML content.
   - Most of the content is stored on disk.
   - Popular content is kept in memory to reduce latency.
- **Link extractor**
   - Parses and extracts links from HTML pages.
- **URL Filter**
   - Excludes certain content types, file extensions, error links and URLs in “blacklisted” sites.
- **URL Storage**
   - Stores already visited URLs.

## Detailed design

