# URL Shortening Service

## Requirements Clarification
- **Functional requirements**
   - URL Shortening (Write): Given an original URL, our service should generate a shorter and unique URL of it.
   - URL Redirection (Read): When users access a short URL, our service should redirect them to the original URL.
   - URL Customization: Users should optionally be able to pick a custom short URL for their original URL.
   - URL Expiration: Shorter URL will expire after a standard default timespan. Users should be able to specify the expiration time.
- **Non-functional requirements**
   - The system should be highly available (ff our service is down, all the URL redirections will start failing).
   - URL redirection should happen in real-time with minimal latency.
   - Shortened links should not be guessable (not predictable).

## Estimation
- **Traffic estimation**
   - Our system will be read-heavy (Lots of redirection requests compared to new URL shortenings).
   - Read-write ratio is 100 : 1 (*Assumed*)
   - Number of read actions and write actions per month
      - Number of writes (URL Shortening) per month = 500 millions (*Assumed*)
      - Number of reads (URL Redirection) per month= 500 millions x 100 = 50 billion
   - Frequency of read actions and write actions per second (QPS)
      - Frequency of writes per second = 500 millions / (30 days x 24 hours x 3600 seconds) = 200 times/s 
      - Frequency of reads per second = 200 times/s x 100 = 20000 times/s
- **Storage estimation**
   - Types
      - Data: Yes
      - File: No
   - Capacity
      - Time length of storing a record = 5 years (*Assumed*)
      - Number of records created in 5 years = Number of writes per month x Number of months = 500 million x 5 years x 12 months = 30 billion
      - Size of one record = 500 bytes (*Assumed*)
      - Total capacity needed in 5 years = 30 billion * 500 bytes = 15 TB
- **Bandwidth estimation**
   - Write bandwidth = Frequency of writes per second x Size of one record = 200 times/s x 500 bytes = 100 KB/s
   - Read bandwidth = Frequency of reads per second x Size of one record = 20000 times/s x 500 bytes = 10 MB/s

## System interface definition
- **Interface 1**
   - `createURL(api_key, original_url, custom_alias=None, user_name=None, expire_date=None)`
      - Function
         - Create a new shorter URL.
      - Parameters
         - api_dev_key (string): The API developer key of a registered account.
         - original_url (string): Original URL to be shortened.
         - custom_alias (string): Optional custom key for the URL.
         - user_name (string): Optional user name to be used in the encoding.
         - expire_date (string): Optional expiration date for the shortened URL.
- **Interface 2**
   - `deleteURL(api_dev_key, short_url)`
      - Function
         - Delete a short URL.
      - Parameters
         - api_dev_key (string): The API developer key of a registered account.
         - short_url (string): The short URL to be deleted.

## Data model definition
- **Schema**
   - Table 1: URL
      - Description
         - Store URL mappings.
      - Columns
        | Column Name | Column Type | PK | Description |
        |----|----|----|----|
        | ShortUrl | varchar(16) | PK | The short URL. |
        | OriginalUrl | varchar(512) | | The original long URL. |
        | CreationDate | datetime | | The creation date of the short URL. |
        | ExpirationDate | datetime | | The expiration date of the short URL. |
        | UserID | int | | The UserID of the user who created this short URL. |
      - Foreign key relationship
         - URL.UserID (n:1) User:UserID
   - Table 2: User
      - Description
         - Store user accounts.
      - Columns
        | Column Name | Column Type | PK | Description |
        |----|----|----|----|
        | UserID | int | PK | The user ID. |
        | Name | varchar(20) | | The name of the user. |
        | Email | varchar(32) | | The email of the user. |
        | CreationDate | datetime | | The creation date of the user. |
        | LastLogin | datetime | | The last login time of the user. |
      - Foreign key relationship
         - URL.UserID (n:1) User:UserID
- **Database**
   - NoSQL
      - Reason
         - No relation need to look up.
         - NoSQL is good at scaling.     

## High-level design
![url](https://user-images.githubusercontent.com/8989447/116921161-da7cd380-ac10-11eb-8216-f05e13335782.png)

## Detailed design
- **Short URL generation server**
   - Considerations
      - Consideration 1: Uniqueness of short URLs.
         - Calculation: Number of unique URLs = Number of all possible characters in one digit<sup>Number of digits</sup>
         - Solutions
            - Solution 1: Only use number (0-9) and short URLs are 7-digit long
               - Number of unique URLs = 10<sup>7</sup> = 10 million
            - Solution 2: Use base36 ([a-z, 0-9]) and short URL are 7-digit long
               - Number of unique URLs = 36<sup>7</sup> = 78 billion
            - Solution 3: Use base62 ([A-Z, a-z, 0-9]) and short URL are 7-digit long
               - Number of unique URLs = 62<sup>7</sup> = 3.5 trillion
      - Consideration 2: Length of short URLs.
         - Basic idea:
            - Keep short URL as short as possible.
            - Don't let unique short URLs run out easily.
 
      
