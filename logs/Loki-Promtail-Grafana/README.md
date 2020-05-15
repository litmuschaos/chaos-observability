# Install eventrouter-loki-grafana stack for visualizing Kubernetes Events


## Step 1:

- Install Loki Grafana and Promtail Stack:
    `$ helm upgrade --install default loki/loki-stack  --set grafana.enabled=true,prometheus.enabled=false,prometheus.alertmanager.persistentVolume.enabled=false,prometheus.server.persistentVolume.enabled=false`

## Step 2:

- After this, we have to just head over Grafana Dashboard, add Loki as an Datasource, by using it's ClusterIP, and then just add this filter, according to the job name of the chaos experiment.
    `$ {job="namespace/chaos-experiment"}`


## Images for Reference:

![](https://github.com/litmuschaos/chaos-observability/blob/master/images/loki-basic-joblogs.png)