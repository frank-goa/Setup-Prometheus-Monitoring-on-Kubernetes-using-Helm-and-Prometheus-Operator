# Setup-Prometheus-Monitoring-on-Kubernetes-using-Helm-and-Prometheus-Operator
Setup Prometheus Monitoring on Kubernetes using Helm and Prometheus Operator

```bash
helm install prometheus prometheus-community/kube-prometheus-stack
```

<img width="1382" alt="Screenshot 2024-01-09 at 09 17 36" src="https://github.com/frank-goa/Setup-Prometheus-Monitoring-on-Kubernetes-using-Helm-and-Prometheus-Operator/assets/137857643/55157ef5-4860-4381-9a35-c8e7295c5df8">

```bash
kubectl get all 
```

<img width="1379" alt="Screenshot 2024-01-09 at 09 18 15" src="https://github.com/frank-goa/Setup-Prometheus-Monitoring-on-Kubernetes-using-Helm-and-Prometheus-Operator/assets/137857643/20f906b2-8a88-499b-bd5b-b86d3f26f634">


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

- prom.yaml
```bash
Name:               prometheus-prometheus-kube-prometheus-prometheus
Namespace:          default
CreationTimestamp:  Tue, 09 Jan 2024 09:11:16 +0000
Selector:           app.kubernetes.io/instance=prometheus-kube-prometheus-prometheus,app.kubernetes.io/managed-by=prometheus-operator,app.kubernetes.io/name=prometheus,operator.prometheus.io/name=prometheus-kube-prometheus-prometheus,operator.prometheus.io/shard=0,prometheus=prometheus-kube-prometheus-prometheus
Labels:             app=kube-prometheus-stack-prometheus
                    app.kubernetes.io/instance=prometheus
                    app.kubernetes.io/managed-by=Helm
                    app.kubernetes.io/part-of=kube-prometheus-stack
                    app.kubernetes.io/version=55.7.0
                    chart=kube-prometheus-stack-55.7.0
                    heritage=Helm
                    operator.prometheus.io/mode=server
                    operator.prometheus.io/name=prometheus-kube-prometheus-prometheus
                    operator.prometheus.io/shard=0
                    release=prometheus
Annotations:        meta.helm.sh/release-name: prometheus
                    meta.helm.sh/release-namespace: default
                    prometheus-operator-input-hash: 14619287190508193130
Replicas:           1 desired | 1 total
Update Strategy:    RollingUpdate
Pods Status:        1 Running / 0 Waiting / 0 Succeeded / 0 Failed
Pod Template:
  Labels:           app.kubernetes.io/instance=prometheus-kube-prometheus-prometheus
                    app.kubernetes.io/managed-by=prometheus-operator
                    app.kubernetes.io/name=prometheus
                    app.kubernetes.io/version=2.48.1
                    operator.prometheus.io/name=prometheus-kube-prometheus-prometheus
                    operator.prometheus.io/shard=0
                    prometheus=prometheus-kube-prometheus-prometheus
  Annotations:      kubectl.kubernetes.io/default-container: prometheus
  Service Account:  prometheus-kube-prometheus-prometheus
  Init Containers:
   init-config-reloader:
    Image:      quay.io/prometheus-operator/prometheus-config-reloader:v0.70.0
    Port:       8080/TCP
    Host Port:  0/TCP
    Command:
      /bin/prometheus-config-reloader
    Args:
      --watch-interval=0
      --listen-address=:8080
      --config-file=/etc/prometheus/config/prometheus.yaml.gz
      --config-envsubst-file=/etc/prometheus/config_out/prometheus.env.yaml
      --watched-dir=/etc/prometheus/rules/prometheus-prometheus-kube-prometheus-prometheus-rulefiles-0
    Environment:
      POD_NAME:   (v1:metadata.name)
      SHARD:     0
    Mounts:
      /etc/prometheus/config from config (rw)
      /etc/prometheus/config_out from config-out (rw)
      /etc/prometheus/rules/prometheus-prometheus-kube-prometheus-prometheus-rulefiles-0 from prometheus-prometheus-kube-prometheus-prometheus-rulefiles-0 (rw)
  Containers:
   prometheus:
    Image:      quay.io/prometheus/prometheus:v2.48.1
    Port:       9090/TCP
    Host Port:  0/TCP
    Args:
      --web.console.templates=/etc/prometheus/consoles
      --web.console.libraries=/etc/prometheus/console_libraries
      --config.file=/etc/prometheus/config_out/prometheus.env.yaml
      --web.enable-lifecycle
      --web.external-url=http://prometheus-kube-prometheus-prometheus.default:9090
      --web.route-prefix=/
      --storage.tsdb.retention.time=10d
      --storage.tsdb.path=/prometheus
      --storage.tsdb.wal-compression
      --web.config.file=/etc/prometheus/web_config/web-config.yaml
    Liveness:     http-get http://:http-web/-/healthy delay=0s timeout=3s period=5s #success=1 #failure=6
    Readiness:    http-get http://:http-web/-/ready delay=0s timeout=3s period=5s #success=1 #failure=3
    Startup:      http-get http://:http-web/-/ready delay=0s timeout=3s period=15s #success=1 #failure=60
    Environment:  <none>
    Mounts:
      /etc/prometheus/certs from tls-assets (ro)
      /etc/prometheus/config_out from config-out (ro)
      /etc/prometheus/rules/prometheus-prometheus-kube-prometheus-prometheus-rulefiles-0 from prometheus-prometheus-kube-prometheus-prometheus-rulefiles-0 (rw)
      /etc/prometheus/web_config/web-config.yaml from web-config (ro,path="web-config.yaml")
      /prometheus from prometheus-prometheus-kube-prometheus-prometheus-db (rw)
   config-reloader:
    Image:      quay.io/prometheus-operator/prometheus-config-reloader:v0.70.0
    Port:       8080/TCP
    Host Port:  0/TCP
    Command:
      /bin/prometheus-config-reloader
    Args:
      --listen-address=:8080
      --reload-url=http://127.0.0.1:9090/-/reload
      --config-file=/etc/prometheus/config/prometheus.yaml.gz
      --config-envsubst-file=/etc/prometheus/config_out/prometheus.env.yaml
      --watched-dir=/etc/prometheus/rules/prometheus-prometheus-kube-prometheus-prometheus-rulefiles-0
    Environment:
      POD_NAME:   (v1:metadata.name)
      SHARD:     0
    Mounts:
      /etc/prometheus/config from config (rw)
      /etc/prometheus/config_out from config-out (rw)
      /etc/prometheus/rules/prometheus-prometheus-kube-prometheus-prometheus-rulefiles-0 from prometheus-prometheus-kube-prometheus-prometheus-rulefiles-0 (rw)
  Volumes:
   config:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  prometheus-prometheus-kube-prometheus-prometheus
    Optional:    false
   tls-assets:
    Type:                Projected (a volume that contains injected data from multiple sources)
    SecretName:          prometheus-prometheus-kube-prometheus-prometheus-tls-assets-0
    SecretOptionalName:  <nil>
   config-out:
    Type:       EmptyDir (a temporary directory that shares a pod's lifetime)
    Medium:     Memory
    SizeLimit:  <unset>
   prometheus-prometheus-kube-prometheus-prometheus-rulefiles-0:
    Type:      ConfigMap (a volume populated by a ConfigMap)
    Name:      prometheus-prometheus-kube-prometheus-prometheus-rulefiles-0
    Optional:  false
   web-config:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  prometheus-prometheus-kube-prometheus-prometheus-web-config
    Optional:    false
   prometheus-prometheus-kube-prometheus-prometheus-db:
    Type:       EmptyDir (a temporary directory that shares a pod's lifetime)
    Medium:     
    SizeLimit:  <unset>
Volume Claims:  <none>
Events:
  Type    Reason            Age   From                    Message
  ----    ------            ----  ----                    -------
  Normal  SuccessfulCreate  53m   statefulset-controller  create Pod prometheus-prometheus-kube-prometheus-prometheus-0 in StatefulSet prometheus-prometheus-kube-prometheus-prometheus successful

```
