---
title: k8s monitoring
draft: false
tags:
  - k8s-monitoring
  - grafana
  - prometheus
date: 2026-03-29
description: all about k8s monitoring using grafana and prometheus!
---
# k8s monitoring

a k8s cluster needs monitoring when it is being used by multiple teams in a organization, as there might be many issues in the cluster and if we have a good monitoring system in place, we can easily identify the issues and resolve them! 2 such tools are Prometheus and Grafana

### Prometheus

- Prometheus is a monitoring tool that fetches all the information about a k8s cluster and monitors the cluster events such as pod, deployment or any other resource failures and can also be used to set up triggers such as alerts and alarms!

```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

helm repo update

helm install prometheus prometheus-community/prometheus

kubectl get pods | grep prometheus
```

- when installed, prometheus creates many pods and services in the cluster that can be used to monitor the cluster for ex we can expose the prometheus server:

```
kubectl expose service prometheus-server --type=NodePort --target-port=9090 --name=prometheus-server-ext
```

- visit http://localhost:30567 to open the prometheus server!

### Grafana

- Grafana is a visualization tool that helps visualize the metrics of the k8s cluster in forms of graphs and charts!

```bash
helm repo add grafana-community https://grafana-community.github.io/helm-charts

helm repo update

helm install grafana grafana-community/grafana
```

- when installed, grafana creates a service in the cluster that can be then exposed to directly access it from the browser

```bash
kubectl expose svc grafana --type=NodePort --target-port=3000 --name=grafana-server-ext

service/grafana-server-ext exposed
```

```bash
 k get secrets -n default grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
```

- use it to decode the password for the grafana application
## Links:

202603292054
