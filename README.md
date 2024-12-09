# Task 9: Alertmanager Configuration and Verification

## Objective

In this task, you will configure Grafana Alerting to send alerts for specific events in your Kubernetes (K8s) cluster and verify that the alerts are received.

## File Structure
- **```grafana```**:
  The directory is where Grafana yaml files are stored.
- **```Screenshots```**:  
  This directory contains screenshots for cross-checking.
- **```cross-check9.md```**:    
  This file is only needed for cross-checking and will make your check easier.


## Steps

1. **Configure SMTP for Grafana**

   To enable email alerts, set up SMTP in Grafana. The configuration varies depending on the environment:

   a. Local Setup
   Use any available SMTP server (e.g., Gmail, Postfix).
   Minimal configuration
   ```
   [smtp]
   enabled = true
   host = "smtp.example.com:587"
   skip_verify = true
   from_address = "grafana@example.com"
   from_name = "Grafana Alerts"
   ```
   Save these settings as part of your Helm chart values.

   b. AWS SES Setup

   Obtain the SMTP credentials and verify a "From Address" in AWS SES.
   Example configuration:
   ```
   [smtp]
   enabled = true
   host = "email-smtp.us-east-1.amazonaws.com:587"
   user = "AWS_SES_ACCESS_KEY"
   password = "AWS_SES_SECRET_KEY"
   from_address = "verified-email@example.com"
   from_name = "Grafana Alerts"
   ```
   Save this configuration securely, ensuring credentials are not exposed.

   Restart Grafana to apply the changes.

2. **Configure Contact points**
   
   - Navigate to Alerting > Contact Points in Grafana.

   - Add a new email contact point:

     - Enter your email address as the recipient.

     - Ensure this email is verified if using AWS SES.

   - Save the contact point and test the configuration.

3. **Configure Alert Rules**

   - Navigate to Alerting > Alert Rules and create two rules:

     - High CPU Utilization:

       - Expression: ```sum(rate(node_cpu_seconds_total{mode="user", instance=~"node.*"}[2m])) * 200```

     - Low RAM Capacity:

       - Expression: ```((sum(node_memory_MemTotal_bytes{instance=~"node.*"}) - sum(node_memory_MemFree_bytes{instance=~"node.*"}) - sum(node_memory_Buffers_bytes{instance=~"node.*"}) - sum(node_memory_Cached_bytes{instance=~"node.*"})) / sum(node_memory_MemTotal_bytes{instance=~"node.*"})) * 100```

     - Link these rules to the contact point created earlier.
       


4. **Verify Alerts**
   - Simulate stress on a Kubernetes node:

       - Install ```stress``` on the node:
       
       ```
       apt-get install stress
       ```

       - Run CPU stress:

       ```
       stress --cpu 2 --timeout 300
       ```

       - Run memory stress:

       ```
       stress --vm 2 --vm-bytes 2G --timeout 300
       ```

   - Monitor the alerts in Grafana:

     - Ensure the alert rules transition to Firing State.

     - Verify that emails are received for the triggered alerts.
