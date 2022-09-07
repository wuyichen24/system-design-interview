# Build Payment System

## Real-life examples

## Requirements clarification
- **Functional requirements**
   - Support money movement for an e-commerce application:
      - Pay-in flow: Receive money from customers on behalf of sellers.
      - Pay-out flow: Send moneyto sellers.
   - Use third-party payment processors (Paypal, Stripe, Square, Braintree, Adyen, Galileo, etc.) for credit card payment processing.
- **Non-functional requirements**
   - Fault tolerance (Failed payments need to be handled carefully).
   - A reconciliation process between internal services (payment services, accounting services, etc.) and external services (When a service fails, different services may run into inconsistent states. So we need to execute the reconciliation process to fix any inconsistent payment information among all services).

## Estimation
- **Traffic estimation**
- **Storage estimation**
- **Bandwidth estimation**

## System interface definition

## Data model definition
- **Schema**
- **Database**

## High-level design

## Detailed design

## References
