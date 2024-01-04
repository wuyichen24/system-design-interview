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
   - Send alert notifications to various alerting destinations.
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

- **Metrics Source**
   - Provides metrics, like application servers, database, message queues.
- **Metrics Collector**
   - Gathers metrics data and writes data into the time-series database.
- **Time-series database**
   - Stores metrics data as time series.
   - Provides a custom query interface for analyzing and summarizing a large amount of time-series data.
   - Maintains indexes on labels to facilitate the fast lookup of time-series data by labels.
- **Query Service**
   - Makes it easy to query and retrieve data from the time-series database.
   - This should be a very thin wrapper if we choose a good time-series database. It could also be entirely replaced by the time-series database’s own query interface.
- **Alerting system**
   - Sends alert notifications to various alerting destinations.

## Detailed design
### Metrics collection
- **Ways of collecting metrics**
   - *Pull model*
      - There are dedicated metric collectors which pull metrics values from the running applications periodically via a pre-defined HTTP endpoint (for example, /metrics).
      - Metrics collectors will query Service Discovery to get the complete list of service endpoints to pull data from.
      - Use a consistent hash ring to decide each metrics collector needs to collect which set of servers.

        <img width="500" alt="pull-model" src="https://github.com/wuyichen24/system-design-interview/assets/8989447/0f36fe3c-8402-4b88-a8f1-3fee983780c8">
        
   - *Push model*
      - A collection agent
          - Commonly installed on every server being monitored.
          - Collects metrics and pushes those metrics periodically to the metrics collector.
      - The metrics collector should be in an auto-scaling cluster with a load balancer in front of it.
     
        <img width="500" alt="push-model" src="https://github.com/wuyichen24/system-design-interview/assets/8989447/46e8f82a-975d-4581-9b7c-f56a1742aecd">

## Key points
