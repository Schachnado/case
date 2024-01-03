# Minikube Kubernetes Setup with Prometheus and Grafana

This repository provides a simple Minikube setup for Kubernetes using Docker as the driver. Minikube simplifies the process of setting up a local Kubernetes environment, making it ideal for this small-scale project. The Kubernetes cluster is also viewable through the Minikube dashboard. To manage packages in Kubernetes, Helm was used to simplify installation and deployment of Prometheus and Grafana. Prometheus collects metrics from the Kubernetes cluster, and Grafana provides a visualization for these metrics.  

## Prerequisites

- [Minikube]
- [kubectl]
- [Helm]
- [Docker/supported VM]

1. Start Minikube:

    ```bash
    minikube start --driver=docker
    ```

2. Install Helm in your Minikube cluster:

    ```bash
    helm repo add stable https://charts.helm.sh/stable
    helm repo update
    ```

3. Deploy Prometheus using Helm:

    ```bash
    helm install prometheus stable/prometheus
    ```

4. Deploy Grafana using Helm:

    ```bash
    helm install grafana stable/grafana
    ```

5. Expose Prometheus-server service:

   ```bash
   kubectl expose service prometheus-server --type=NodePort --target-port=9090 --name=prometheus-server-ext
    ```

7. Expose Grafana service

    ```bash
    kubectl expose service grafana --type=NodePort --target-port=3000 --name=grafana-ext
    ```

8. Run Prometheus service

   ```bash
   minikube service prometheus-server-ext
   ```

9. Run Grafana service

   ```bash
   minikube service grafana-ext
   ```

