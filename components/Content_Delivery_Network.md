# Content Delivery Network

## Concepts
- Geographically distributed network of proxy servers and their data centers.

  ![what-is-a-cdn](https://user-images.githubusercontent.com/8989447/149716692-5b91acd3-09a0-4773-a818-0c22429038da.png)

## Functionalities
- Serve content from locations closer to the user.

## Pros
- High availability.
- Better performance.

## Cons
- CDN costs could be significant.
- Content might be stale.
- CDNs require changing URLs for static content to point to the CDN.

## Types
- Push
   - You upload new content from your server to CDN when the content is new or changed.
     
     ![push](https://user-images.githubusercontent.com/8989447/149717231-8acab97d-ec06-4e6a-96b0-60b81f0bf3b0.png)
- Pull
   - CDN grabs new content from your server to itself when the first user requests the content.

     ![pull](https://user-images.githubusercontent.com/8989447/149717254-17fea23f-934b-4684-8531-bea03a079069.png)
