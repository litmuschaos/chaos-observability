
# Install chaosexporter-prometheus-grafana stack for visualizing Litmus metrics

- All the steps in this guide deploys the stack in Litmus Namespace and require Litmus Service Account to be created. (`kubectl apply -f https://litmuschaos.github.io/pages/litmus-operator-v1.4.0.yaml`). 
Ref: <a href="https://docs.litmuschaos.io/docs/faq-general/#what-are-the-permissions-required-to-run-litmus-chaos-experiments">FAQ</a>


## Step 1:

- Install Chaos Exporter  
    `$ kubectl apply -f https://raw.githubusercontent.com/litmuschaos/chaos-exporter/master/deploy/chaos-exporter.yaml`

## Step 2:

- Install Prometheus to use chaos exporter service:
    `$ kubectl apply -f ./utils/prometheus-manifests.yaml`

## Step 3:

- After this, use Grafana to visualize Kubernetes Events send by Prometheus
    `$ kubectl apply -f ./litmus-grafana.yaml`

## Step 4:

- Head over to Grafana, to see the metrics by using Prometheus as a sink and view the chaos exporter.
