# Task 7: Prometheus Deployment on K8s

## Objective

In this task, you will install Prometheus on your Kubernetes (K8s) cluster using a Helm chart and configure it to collect essential cluster-specific metrics.

## File Structure
- **```.github/workflows/```**:
  The directory is where GitHub-specific files are stored, particularly workflows for GitHub Actions.
- **```helm/prometheus-values.yaml```**:  
  Configuration file of Prometheus Helm chart

## Steps

1. **Install Prometheus**
   - Prometheus can be deployed using the Bitnami Helm chart. Ensure Helm is installed and configured to communicate with your Kubernetes cluster.

   ```
   helm upgrade --install my-release oci://registry-1.docker.io/bitnamicharts/prometheus --namespace monitoring --create-namespace
   ```
   Replace ```my-release``` with your desired release name.
   This command installs Prometheus with default configuration. Refer to the [Bitnami Prometheus Chart Documentation](https://prometheus.io/docs/introduction/overview/) for more details on configuration options.
   
   If custom parameters are needed, create a values.yaml file and install Prometheus using:
   ```
   helm install prometheus oci://registry-1.docker.io/bitnamicharts/prometheus -f helm/prometheus-values.yaml --namespace monitoring --create-namespace
   ```

2. **Install Exporters**
   - Exporters are essential for collecting metrics from Kubernetes components and other services. Some recommended exporters include:

     - **Node Exporter:** Collects node-level metrics.

     ```
     helm install node-exporter oci://registry-1.docker.io/bitnamicharts/prometheus-node-exporter --namespace monitoring
     ```

     - **Kube-State-Metrics:** Exposes Kubernetes cluster state metrics.
     
     ```
     helm install kube-state-metrics oci://registry-1.docker.io/bitnamicharts/kube-state-metrics --namespace monitoring
     ```

3. **Configure Prometheus**
   - Customize Prometheus to scrape metrics from the installed exporters by editing the configuration file. Update the values.yaml file for the Helm chart or use ```--set``` flags during installation/upgrades.
   
   - Example for adding a scrape target:
     
     ``` yaml
     extraScrapeConfigs: | 
       - job_name: 'kubernetes-nodes'
         static_configs:
         - targets: ['<node-exporter-service>:9100']
       - job_name: 'kubernetes-kube-state'
         static_configs:
         - targets: ['<kube-state-metrics-service>:8080']
     ```
    
    - Apply the updated configuration:

    ```
    helm upgrade prometheus oci://registry-1.docker.io/bitnamicharts/prometheus -f helm/prometheus-values.yaml
    ```



4. **Verify Metrics Collection**
   
    After deployment, verify that Prometheus is collecting metrics as expected.

    **Access the Prometheus Web Interface**
    Forward the Prometheus server port:

    ```
    kubectl port-forward svc/prometheus-server 9090:80 -n monitoring
    ```
   
    Open a browser and navigate to ```http://localhost:9090```.

    **Query Essential Metrics**

    Use Prometheus' query interface to verify the collection of key metrics. Examples:

      - Node Memory Usage: ```node_memory_Active_bytes```

      - CPU Usage: ```rate(node_cpu_seconds_total[5m])```

      - Pod Status: ```kube_pod_status_phase```


     Access to Prometheus is secured through Nginx proxying, with the added protection of a Let's Encrypt certificate. Nginx is installed on the bastion host and is configured to proxy only Grafana, not Prometheus. This setup provides an additional layer of protection for Prometheus, effectively preventing unauthorized access to the application.

     URL for accessing Grafana: https://rs-test.cloudns.cl/
