## Evaluation Criteria (100 points for covering all criteria)

1. **Contact Points created (10 points)**

    ![](Screenshots/01.png)

    ![](Screenshots/02.png)


2. **Alert Rules created (40 points)**
   - Alert Rules are configured to send alerts for the following events:
     - High CPU utilization on any node of the cluster.
     - Lack of RAM capacity on any node of the cluster.
       
       https://github.com/CiscoSA/rs-prometheus/blob/task_9/grafana/alerts.yaml

    ![](Screenshots/03.png)

    ![](Screenshots/04.png)

   - Alerts are configured to be delivered to your email address.

     !!! TODO !!!

3. **Alert Rules are working as expected (20 points)**
   - Alert Rules are firing when the specified events occur.

    ![](Screenshots/06.png)

    ![](Screenshots/07.png)       

4. **Email is received (10 points)**

    ![](Screenshots/10.png)

    ![](Screenshots/11.png)

    ![](Screenshots/12.png)

    ![](Screenshots/13.png)

    ![](Screenshots/14.png)

5. **Additional Tasks (20 points)**
   - **Documentation (10 points)**
     - The Alertmanager setup and alert configuration are documented in a README file.

       https://github.com/CiscoSA/rs-prometheus/blob/task_9/README.md

   - **Configuration is done completely in code (10 points)**

     - Alert Rules, Contact Points, and SMTP settings are configured using YAML files or other code-based methods.
       
       https://github.com/CiscoSA/rs-prometheus/blob/task_9/grafana/alerts.yaml

       https://github.com/CiscoSA/rs-prometheus/blob/task_9/grafana/contact.yaml

       https://github.com/CiscoSA/rs-prometheus/blob/task_9/grafana/dashboard.yaml

       https://github.com/CiscoSA/rs-prometheus/blob/task_9/grafana/smtp.yaml
