
# Install metricbeat-elasticsearch-kibana stack for visualizing Kubernetes Events

## Step 1:

- Install ElasticSearch from it's official Repository (https://www.elastic.co/blog/alpha-helm-charts-for-elasticsearch-kibana-and-cncf-membership):
    `$ helm repo add elastic https://helm.elastic.co`
    `$ helm install --name elasticsearch elastic/elasticsearch`

## Step 2:

- Install Kibana:
    `$ helm install --name kibana elastic/kibana`

## Step 3:

- After this, we have to metricbeat and its configration to get Kubernetes Events
    `$ kubectl apply -f ./0-metricbeat.yaml`

## Step 4:

- Head over to Kibana, and add metricbeat index, and view the Kubernetes events.

## Step 5:

- If you want to just view Chaos Metrics, please add this filter:
    `kubernetes.event.involved_object.kind: ChaosEngine`

### Images for reference:

![](images/kibana-display-filter.png)
![](images/kibana-edit-filter.png)
