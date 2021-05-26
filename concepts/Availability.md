# Availability

## Solutions for enhancing availability
- **Cold Standby**
   - Use heartbeat or metrics/alerts to track failure. Provision new standby nodes when a failure occurs. 
   - Only suitable for stateless services.
- **Warm Standby**
   - Keep two active systems but the secondary one does not take traffic unless the failure occurs.
- **Hot Standby**
   - Keep two active systems undertaking the same role. Data is mirrored in near real time, and both systems will have identical data.
- **Active-active**
   - Keep two active systems behind a load balancer. Both of them take in parallel. Data replication is bi-directional.
