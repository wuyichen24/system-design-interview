# Build Notification System

## Requirements clarification
- **Functional requirements**
   - System can send push notifications, SMS messages and emails.
   - Notifications can be triggered by server-side and client-side.
- **Non-functional requirements**

## High-level design

![figure-10-10-VPOYUWTG](https://github.com/wuyichen24/system-design-interview/assets/8989447/a244bfab-f0ee-4875-ab68-2ce001d73fc7)

- **Service 1 to N**
   - Different services that send notifications via APIs provided by notification servers.
- **Notification servers**
   - Provides APIs for services to send notifications.
   - Queries the database or cache to fetch data needed to render a notification.
   - Carries out basic validations to verify emails, phone numbers.
   - Puts notification data to message queues for parallel processing.
- **Cache**
   - Caches user info, device info, notification templates.
- **DB**
   - Stores user info, device info, notification templates.
- **Message queues**
   - Buffers notifications need to be sent out for different types.
- **Workers**
   - A list of servers that pull notification events from message queues and send them to the corresponding third-party services.
- **Third-party services**
   - *APNs (Apple Push Notification Service)*
      - For iOS push notifications.
   - *FCM (Firebase Cloud Messaging)*
      - For Android push notifications.
      - Examples for China: Jpush, PushY.
   - *SMS Service*
      - Examples: Twilio, Nexmo, AWS SNS.
   - *Email Service*
      - Examples: Sendgrid, Mailchimp, AWS SES.

## Detailed Design
### Updated design for considering other factors

![figure-10-14-XSG2DEDM](https://github.com/wuyichen24/system-design-interview/assets/8989447/cc85002f-d395-44b4-8e3a-615d67616837)
