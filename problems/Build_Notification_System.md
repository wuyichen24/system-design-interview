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
   - Provide APIs for services to send notifications.
   - Query the database or cache to fetch data needed to render a notification.
   - Carry out basic validations to verify emails, phone numbers.
   - Put notification data to message queues for parallel processing.
