# Build Payment System

## Real-life examples

## Requirements clarification
- **Functional requirements**
   - Support money movement for an e-commerce application:
      - Pay-in flow: Receive money from customers on behalf of sellers.
      - Pay-out flow: Send money to sellers.

        ![pay-in-out](https://user-images.githubusercontent.com/8989447/188941477-5734acbe-5aba-4820-a252-990291c5fa3c.png)

   - Use third-party payment processors (Paypal, Stripe, Square, Braintree, Adyen, Galileo, etc.) for credit card payment processing.
- **Non-functional requirements**
   - Fault tolerance (Failed payments need to be handled carefully).
   - A reconciliation process between internal services (payment services, accounting services, etc.) and external services (payment service providers, etc.)
      - When a service fails, different services may run into inconsistent states. So we need to execute the reconciliation process to fix any inconsistent payment information among all services.

## Estimation
- **Traffic estimation**
- **Storage estimation**
- **Bandwidth estimation**

## System interface definition

## Data model definition
- **Schema**
- **Database**

## High-level design

![4d94e3eb-6f7b-4688-825f-c4e88e6c0d74_1913x1536](https://user-images.githubusercontent.com/8989447/188942625-263b3312-0d2d-4111-adc0-e3d8a4040cf8.jpeg)

- **Components**
   - Payment service
      - Accepts payment events (one event may contain multiple payment orders) from users and coordinates the payment process.
   - Payment executor
      - Executes a single payment order via a Payment Service Provider (PSP).
   - Payment Service Provider (PSP)
      - Moves money from one account to another.
   - Card schemas
      - The organizations that process credit card operations.
   - Ledger
      - Stores transaction history.
   - Wallet
      - Stores accounts' balances.
- **Processes**
   - Process after a user clicks the "place order" button:


## Detailed design

## References
