
# Install eventrouter-prometheus-grafana stack for visualizing Kubernetes Events

## All the steps in this guide deploys the stack in Litmus Namespace and require Litmus Service Account to be created. (kubectl apply -f https://litmuschaos.github.io/pages/litmus-operator-v1.3.0.yaml). 
Ref: https://docs.litmuschaos.io/docs/faq-general/#what-are-the-permissions-required-to-run-litmus-chaos-experiments


## Step 1:

- Install EventRouter via 
    `$ kubectl apply -f ./1-litmus-eventrouter.yaml`

## Step 2:

- Install Prometheus to use EventRouter service:
    `$ kubectl apply -f ./2-litmus-eventrouter-prom.yaml`

## Step 3:

- After this, use Grafana to visualize Kubernetes Events send by Prometheus
    `$ kubectl apply -f ./2-litmus-grafana.yaml`

## Step 4:

- Head over to Grafana, to see the events by using Prometheus as a sink and view the Kubernetes events.