# Build Auction System

## Real-life examples
- eBay

## Requirements clarification
- **Functional requirements**
   - Users should be able to put items up for auction.
   - Bidder's should be able to search for items they are interested in.
   - Bidders should be able to bid on items they are interestes in.
 
- **Non-functional requirements**
   - Low Latency
   - High Availability
   - Highly consistent
      - The bidding part should be highly consistent. Bidders shouldn't be able to bid on unavailable items
      - New items can take some time before they become available for bidders to bid upon

## Estimation
- **Traffic estimation**
   - Our system will be read-heavy.
- **Storage estimation**
- **Bandwidth estimation**

## System interface definition
- Users who want to list new items for auction:
   - putItem(string userId, string itemCategory, int totalQuantity, string description)
   - POST /api/v1/bid?
      - JSON: {userId: "", itemCategory: "", totalQuantity: "", description:""}
- Users who want to bid for an item:
   - bidItem(string userId, string itemId, int quantity, int maxBid}
   - POST /api/v1/bid?
      - JSON {userId: "", itemId: "", totalQuantity: "", maxBid: ""}

## Data model definition
- **Schema**
- **Database**

## High-level design

## Detailed design

## References
- https://leetcode.com/discuss/interview-question/system-design/792060/bidding-system-system-design-interview
