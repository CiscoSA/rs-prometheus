## Evaluation Criteria (100 points for covering all criteria)

1. **Prometheus Installation (20 points)**
   - Prometheus is installed and running on the K8s cluster.

    - https://github.com/CiscoSA/rs-prometheus/actions/runs/12099099331/job/33736300042#step:7:7

    ![](Screenshots/01.png)

2. **Deployment Automation (30 points)**
   - Automation of deployment with IaC or CI/CD pipeline is created.

  - https://github.com/CiscoSA/rs-prometheus/pull/1

  - https://github.com/CiscoSA/rs-prometheus/blob/task_7/.github/workflows/deploy.yml

3. **Web interface is available (10 points)**
   - Metrics can be checked via Prometheus web interface.

  ![](Screenshots/02.png)
  ![](Screenshots/03.png)
  ![](Screenshots/07.png)
  ![](Screenshots/08.png)
  ![](Screenshots/09.png)
  ![](Screenshots/10.png)

4. **Metrics Collection (35 points)**
   - Prometheus is collecting essential cluster-specific metrics, such as nodes' memory usage.

  ![](Screenshots/04.png)
  ![](Screenshots/05.png)
  ![](Screenshots/06.png)


5. **Documentation is created (5 points)**
   - A README file is created or updated documenting the Prometheus deployment and configuration.

     - https://github.com/CiscoSA/rs-prometheus/blob/task_7/README.md