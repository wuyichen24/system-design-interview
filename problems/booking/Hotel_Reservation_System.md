# Build Hotel Reservation System

## Real-life examples
- Airbnb
- Priceline
- Booking.com

## Requirements clarification
- **Functional requirements**
   - Users can search hotels.
   - Users can see detailed pages about hotels and rooms.
   - Users can reserve a room.
   - Hotel owners can use admin portal to add/remove/update hotel or room info.
- **Non-functional requirements**
   - *High concurrency*
      - During peak season or big events, some popular hotels may have a lot of customers trying to book the same room.
   - *Moderate latency*
      - It’s acceptable if the system takes a few seconds to process a reservation request.

## High-level design

![figure-4-high-level-design-4TSKHYJP](https://github.com/wuyichen24/system-design-interview/assets/8989447/aaaaa998-4e4c-4691-85f9-208f3d6bb93e)

### Public
- **Public API Gateway**
   - Directs requests to specific services based on the endpoints.
   - Supports rate limiting, authentication, etc.

- **Hotel Service**
   - Provides detailed information on hotels and rooms.
- **Rate Service**
   - Provides room rates for different future dates.
- **Reservation Service**
   - Receives reservation requests and reserves the hotel rooms.
   - Tracks room inventory as rooms are reserved or reservations are canceled.
- **Payment Service**
   - Executes payment from a customer and updates the reservation status.

### Private
- **Internal APIs**
   - Only available to authorized hotel staff.
   - They are accessible through internal software or websites and protected by a VPN (virtual private network).
- **Hotel Management Service**
   - View the record of an upcoming reservation
   - Reserve a room for a customer
   - Cancel a reservation
