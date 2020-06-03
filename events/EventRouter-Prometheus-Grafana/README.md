
## Monitoring Chaos Events on Grafana

### PreRequisites  
  
This guide assumes that you already have the: 

- Litmus infrastructure in place: 
  - LitmusChaos CRDs installed
  - Chaos Operator running 
  - The desired experiment CR created (in the app namespace or the admin namespace) 
  
  If not, please refer to the [litmus docs](https://docs.litmuschaos.io) for detailed steps to achieve the same
  
- A sample application, say nginx, whose availability we can monitor while it undergoes chaos. If you don't have it installed 
  already, you can execute this command: 
  
  ```
  kubectl apply -f https://raw.githubusercontent.com/litmuschaos/chaos-observability/master/sample-application/nginx.yaml
  ```
  

### Steps to Setup Chaos Events Visualization
  

## Step 1:

- Install HeptioLabs' [eventrouter](https://github.com/heptiolabs/eventrouter)

kubectl apply -f https://raw.githubusercontent.com/litmuschaos/chaos-observability/master/events/EventRouter-Prometheus-Grafana/1-litmus-eventrouter.yaml

(Helps push kubernetes events to metrics endpoint)

## Step 2:  

- Install the Prometheus Blackbox exporter 

kubectl apply -f https://raw.githubusercontent.com/litmuschaos/chaos-observability/master/events/EventRouter-Prometheus-Grafana/2-prometheus-blackbox-exporter.yaml
  
(Helps convert service availability as a prometheus metric) 

## Step 3:

- Install Prometheus to pull the app service & chaos metrics from the blackbox exporter & eventrouter sources respectively

kubectl apply -f https://raw.githubusercontent.com/litmuschaos/chaos-observability/master/utils/prometheus-manifests.yaml

***Note: By default the blackbox exporter scrape job looks for the nginx service, can be modify according to the requirement***

```yaml

static_configs:

- targets:

- 'nginx.default.svc.cluster.local:80'

```

## Step 4:

- Install grafana dashboard, datasource configmaps

- kubectl apply -f https://raw.githubusercontent.com/litmuschaos/chaos-observability/master/events/EventRouter-Prometheus-Grafana/3-grafana-dashboards.yaml

- kubectl apply -f https://raw.githubusercontent.com/litmuschaos/chaos-observability/master/events/EventRouter-Prometheus-Grafana/4-grafana_dashboard_provision.yaml

- kubectl apply -f https://raw.githubusercontent.com/litmuschaos/chaos-observability/master/events/EventRouter-Prometheus-Grafana/5-grafana_datasource_provision.yaml


## Step 5:

- After this, create the grafana deployment & use it to visualize chaos events pulled by `Prometheus` 

kubectl apply -f https://raw.githubusercontent.com/litmuschaos/chaos-observability/master/events/EventRouter-Prometheus-Grafana/6-grafana_deployment.yaml

## Step 6:
 
- Head over to Grafana, to see the events by using Prometheus as a sink and view the Kubernetes events.  

![](https://github.com/litmuschaos/chaos-observability/blob/master/images/events-grafana-dashboard.png)
