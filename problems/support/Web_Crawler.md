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
### Workflow
<img width="800" alt="workflow" src="https://github.com/wuyichen24/system-design-interview/assets/8989447/daeb3eac-4f49-4a73-ae1b-643d81d67b8c">

- Step 1: Add seed URLs to the URL Frontier
- Step 2: HTML Downloader fetches a list of URLs from URL Frontier.
- Step 3: HTML Downloader gets IP addresses of URLs from DNS resolver and starts downloading.
- Step 4: Content Parser parses HTML pages and checks if pages are malformed.
- Step 5: After content is parsed and validated, it is passed to the “Content Seen?” component.
- Step 6: “Content Seen” component checks if a HTML page is already in the storage.
- If it is in the storage, this means the same content in a different URL has already been processed. In this case, the HTML page is discarded.
- If it is not in the storage, the system has not processed the same content before. The content is passed to Link Extractor.
- Step 7: Link extractor extracts links from HTML pages.
- Step 8: Extracted links are passed to the URL filter.
- Step 9: After links are filtered, they are passed to the “URL Seen?” component.
- Step 10: “URL Seen” component checks if a URL is already in the storage, if yes, it is processed before, and nothing needs to be done.
- Step 11: If a URL has not been processed before, it is added to the URL Frontier.

### Algorithm
- **Choice**
   - BFS (DFS is usually not a good choice because the depth of DFS can be very deep).
