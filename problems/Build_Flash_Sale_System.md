# Build Flash Sale System

## Requirements clarification
- **Functional requirements**
- **Non-functional requirements**
   - High availability
   - High concurrency
   - Quick responsiveness

## High-level design

![d1c87ed2-9736-4da1-8b03-6a04eb39e915_2496x2136](https://user-images.githubusercontent.com/8989447/188700350-70526e61-9b01-4e69-8d72-fd0f9686a012.jpeg)

- **Frontend**
   - Performance
      - Less element on the web page.
      - Less JavaScript loading.
      - Pagination: Don't load all the inventory at once, dynamically load more inventory when a user scrolls down the web page.
      - Store static contents in CDN.
   - Security
      - Use [reCAPTCHA](https://en.wikipedia.org/wiki/ReCAPTCHA) before placing an order to prevent robots.
- **Backend**
   - Availability
      - Use isolated instances for flash sale (If the flash sale instances go down, other normal instances will not be affected).
      - Use isolated cache for flash sale (If the flash sale cache goes down, other normal cache will not be affected).
   - Performance
      - Keep inventory data in the cache.
      - Use message queue for asynchronous processing.
      - Less dependencies on other services.
      - Less RPC.
   - Over sale prevention
      - Lock the inventory when placing an order. Decreasing the inventory after payment is successfull.
   - Security
      - Rate limit on a single IP.
      - Anti-DDoS
      - Ban suspicious IPs.
