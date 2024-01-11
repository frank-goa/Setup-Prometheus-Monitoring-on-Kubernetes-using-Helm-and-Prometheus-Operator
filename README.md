# Setup-Prometheus-Monitoring-on-Kubernetes-using-Helm-and-Prometheus-Operator
- Setup Prometheus Monitoring on Kubernetes using Helm and Prometheus Operator (https://www.youtube.com/watch?v=QoDqxm7ybLc&t=28s)


```bash
helm install prometheus prometheus-community/kube-prometheus-stack
kubectl get all 
```

<img width="1390" alt="Screenshot 2024-01-11 at 15 40 43" src="https://github.com/frank-goa/Setup-Prometheus-Monitoring-on-Kubernetes-using-Helm-and-Prometheus-Operator/assets/137857643/29f68863-13a5-434b-83e1-c346932b4b15">



## Big Picture...
- We have the complete monitoring stack setup
- Out of the box monitoring configuration for your K8s Cluster
- Worker Nodes & statistics on worker nodes are being monitored
- Components such as Pods, Deployments, Replica Sets, Stateful Sets are also being monitored

## This is where the configuration comes from...

<img width="1372" alt="Screenshot 2024-01-09 at 09 43 20" src="https://github.com/frank-goa/Setup-Prometheus-Monitoring-on-Kubernetes-using-Helm-and-Prometheus-Operator/assets/137857643/227d3753-cac5-4e1b-9adc-9df481b9ff0a">

## This is where the secrets comes from...
- for Grafana, Prometheus
- includes certificates
- Username & passwords for different UI
  
<img width="1372" alt="Screenshot 2024-01-09 at 09 53 20" src="https://github.com/frank-goa/Setup-Prometheus-Monitoring-on-Kubernetes-using-Helm-and-Prometheus-Operator/assets/137857643/c3c3fcb3-5606-4343-8666-373138f0db50">

## Custom Resource Definations (CRD) also created
- (Extention of K8s API)

<img width="1368" alt="Screenshot 2024-01-09 at 09 59 21" src="https://github.com/frank-goa/Setup-Prometheus-Monitoring-on-Kubernetes-using-Helm-and-Prometheus-Operator/assets/137857643/20187bb9-d800-4ee9-944a-04ec387484fb">

## What is inside of:
- Prometheus
- Allert Manager
- Operator

<img width="1374" alt="Screenshot 2024-01-09 at 10 04 43" src="https://github.com/frank-goa/Setup-Prometheus-Monitoring-on-Kubernetes-using-Helm-and-Prometheus-Operator/assets/137857643/496a7057-5a6e-444d-b06a-5e46ad3b213e">

## How to access Grafana:
```bash
kubectl get service
```
<img width="1380" alt="Screenshot 2024-01-11 at 04 05 39" src="https://github.com/frank-goa/Setup-Prometheus-Monitoring-on-Kubernetes-using-Helm-and-Prometheus-Operator/assets/137857643/97a99de4-c266-4d53-b11b-95bb63f70836">

(Prometheus-grafana is the main UI) - but it is using ClusterIP -
In production environments, it is done using Ingress.
In our case in lab environment, we will access Grafana using pord-forward

<img width="1372" alt="Screenshot 2024-01-11 at 04 07 18" src="https://github.com/frank-goa/Setup-Prometheus-Monitoring-on-Kubernetes-using-Helm-and-Prometheus-Operator/assets/137857643/2317c05a-da07-49ef-86fd-eeb4afbb9b43">

---
---

<img width="1377" alt="Screenshot 2024-01-11 at 04 23 20" src="https://github.com/frank-goa/Setup-Prometheus-Monitoring-on-Kubernetes-using-Helm-and-Prometheus-Operator/assets/137857643/79d70937-1111-49df-9c29-94e9cd2fca6c">

---
### Enabling Port-Forward for Grafana on Port 3000

<img width="1372" alt="Screenshot 2024-01-11 at 04 24 46" src="https://github.com/frank-goa/Setup-Prometheus-Monitoring-on-Kubernetes-using-Helm-and-Prometheus-Operator/assets/137857643/7da60a06-8d6d-4fb6-93d2-c4d025b9feaf">

---
### Accessng Grafana - http://127.0.0.1:3000/

<img width="1510" alt="Screenshot 2024-01-11 at 04 27 00" src="https://github.com/frank-goa/Setup-Prometheus-Monitoring-on-Kubernetes-using-Helm-and-Prometheus-Operator/assets/137857643/5b8a121d-344f-4498-b424-ad33f5b0ddb6">

---
### Enabling Port-Forward for Prometheus on Port 9090

<img width="1375" alt="Screenshot 2024-01-11 at 04 30 57" src="https://github.com/frank-goa/Setup-Prometheus-Monitoring-on-Kubernetes-using-Helm-and-Prometheus-Operator/assets/137857643/b30e389d-1afa-4615-8e19-6a7d21ba0ceb">

---
### Accessng Prometheus - http://127.0.0.1:9090/

<img width="1512" alt="Screenshot 2024-01-11 at 04 31 48" src="https://github.com/frank-goa/Setup-Prometheus-Monitoring-on-Kubernetes-using-Helm-and-Prometheus-Operator/assets/137857643/5ff7b2cb-9cca-43d3-bad7-8930c7363ac0">

