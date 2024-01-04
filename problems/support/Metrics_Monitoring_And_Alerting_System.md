# Metrics Monitoring and Alerting System

## Real-life examples
- Datadog
- New Relic
- Prometheus
- Grafana

## Requirements clarification
- **Functional requirements**
   - Collect a variety of metrics
      - CPU usage
      - Request count
      - Memory usage
      - Message count in message queues
   - Alert users in multiple ways when a metric goes above the threshold
      - Email
      - Phone
      - PagerDuty
      - Webhooks
   - Support metrics visualization
   - Data retention policy:
      - Raw form for 7 days.
      - 1-minute resolution for 30 days.
      - 1-hour resolution for 1 year.
- **Non-functional requirements**
   - Scalability: The system should be scalable to accommodate growing metrics and alert volume.
   - Low latency: The system needs to have low query latency for dashboards and alerts.
   - Reliability: The system should be highly reliable to avoid missing critical alerts.
   - Flexibility: Technology keeps changing, so the pipeline should be flexible enough to easily integrate new technologies in the future.

## Estimation

## System interface definition

## Data model definition

## High-level design
<img width="800" alt="high-level" src="https://github.com/wuyichen24/system-design-interview/assets/8989447/eb54e336-26a6-44a9-a44a-98fbbacb3885">

## Detailed design

## Key points
