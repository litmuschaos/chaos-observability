
  

## Install eventrouter-prometheus-grafana stack for visualizing Kubernetes Events

  

#### All the steps in this guide deploys the stack in Litmus Namespace and require Litmus Service Account to be created.

>  `kubectl apply -f https://litmuschaos.github.io/pages/litmus-operator-v1.4.0.yaml`

  

Ref: <a  href="https://docs.litmuschaos.io/docs/faq-general/#what-are-the-permissions-required-to-run-litmus-chaos-experiments"> FAQ</a>

  
  

## Step 1:

  

- Install EventRouter via

kubectl apply -f <a  href="https://raw.githubusercontent.com/litmuschaos/chaos-observability/master/events/EventRouter-Prometheus-Grafana/1-litmus-eventrouter.yaml"  target="_blank"  >1-litmus-eventrouter.yaml</a>

  

## Step 2:

  

- Install Prometheus blackbox exporter.yml

kubectl apply -f <a  href="https://raw.githubusercontent.com/litmuschaos/chaos-observability/master/events/EventRouter-Prometheus-Grafana/2-prometheus-blackbox-exporter.yaml"  target="_blank">2-prometheus-blackbox-exporter.yaml</a>

  
  

## Step 3:

  

- Install Prometheus to use EventRouter service:

kubectl apply -f <a  href="https://raw.githubusercontent.com/litmuschaos/chaos-observability/master/utils/prometheus-manifests.yaml"  target="_blank">prometheus-manifests.yaml</a>

  

***Note: By default the blackbox exporter scrape job looking for the nginx service, can be modify according to the requirement***

```yaml

static_configs:

- targets:

- 'nginx.default.svc.cluster.local:80'

```

A sample nginx application can be deployed by applying

kubectl apply -f <a href="https://raw.githubusercontent.com/litmuschaos/chaos-observability/master/sample-application/nginx.yaml" target="_blank">nginx-deployment.yml</a>

## Step 4:

  

- Install grafana dasboard, datasource configmaps

- kubectl apply -f <a  href="https://raw.githubusercontent.com/litmuschaos/chaos-observability/master/events/EventRouter-Prometheus-Grafana/3-grafana-dashboards.yaml"  target="_blank">3-grafana-dashboards.yaml</a>

- kubectl apply -f <a  href="https://raw.githubusercontent.com/litmuschaos/chaos-observability/master/events/EventRouter-Prometheus-Grafana/4-grafana_dashboard_provision.yaml"  target="_blank">4-grafana-dashboard_provision.yaml</a>

- kubectl apply -f <a  href="https://raw.githubusercontent.com/litmuschaos/chaos-observability/master/events/EventRouter-Prometheus-Grafana/5-grafana_datasource_provision.yaml"  target="_blank">5-grafana-datasource_provision.yaml</a>

  

## Step 5:

  

- After this, use Grafana to visualize Kubernetes Events pull by `Prometheus`

kubectl apply -f <a  href="https://raw.githubusercontent.com/litmuschaos/chaos-observability/master/events/EventRouter-Prometheus-Grafana/6-grafana_deployment.yaml"  target="_blank">6-grafana_deployment.yaml</a>

## Step 6:

  

- Head over to Grafana, to see the events by using Prometheus as a sink and view the Kubernetes events.

  

![](https://github.com/litmuschaos/chaos-observability/blob/master/images/events-grafana-dashboard.png)