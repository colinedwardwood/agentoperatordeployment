# Grafana Agent on Kubernetes Operator Mode

## Setup Infra

`eksctl create cluster -f eks-cluster.yaml`

## Follow the Docs

### Set up without Helm

Instructions

<https://grafana.com/docs/grafana-cloud/monitor-infrastructure/kubernetes-monitoring/configuration/configure-infrastructure-manually/k8s-agent-operator/>

0. Create the namespace

    `kubectl create namespace grafana`

1. Deploy the CRDs by running the following:

    ```bash
    kubectl create -f https://raw.githubusercontent.com/grafana/agent/main/production/operator/crds/monitoring.coreos.com_podmonitors.yaml \
      -f https://raw.githubusercontent.com/grafana/agent/main/production/operator/crds/monitoring.coreos.com_probes.yaml \
      -f https://raw.githubusercontent.com/grafana/agent/main/production/operator/crds/monitoring.coreos.com_servicemonitors.yaml \
      -f https://raw.githubusercontent.com/grafana/agent/main/production/operator/crds/monitoring.grafana.com_grafanaagents.yaml \
      -f https://raw.githubusercontent.com/grafana/agent/main/production/operator/crds/monitoring.grafana.com_integrations.yaml \
      -f https://raw.githubusercontent.com/grafana/agent/main/production/operator/crds/monitoring.grafana.com_logsinstances.yaml \
      -f https://raw.githubusercontent.com/grafana/agent/main/production/operator/crds/monitoring.grafana.com_metricsinstances.yaml \
      -f https://raw.githubusercontent.com/grafana/agent/main/production/operator/crds/monitoring.grafana.com_podlogs.yaml
    ```

2. Deploy the operator by applying the following manifest:

    `kubectl apply -f grafana-agent-operator.yaml`

3. Create the access token for my cluster.  

4. Deploy kube-state-metrics to your cluster  

    `kubectl apply -f kube-state-metrics.yaml`

5. Deploy grafana agent to your cluster

    `kubectl apply -f grafana-agent.yaml`

6. Deploy custom resources to collect metrics

    `kubectl apply -f custom-resource-metrics.yaml`

7. Deploy custom resources to collect logs

    `kubectl apply -f custom-resource-logs.yaml`

8. Deploy eventhandler to collect events

    `kubectl apply -f event-handler.yaml`

9. Deploy custom resources to collect cost metrics

    `kubectl apply -f custom-resource-cost-metrics.yaml`

10. Clean up

    `eksctl delete cluster --name cew-dev-cluster --region ca-central-1`

11. All in one

    ```bash
    eksctl create cluster -f eks-cluster.yaml
    kubectl create namespace grafana
    kubectl create -f https://raw.githubusercontent.com/grafana/agent/main/production/operator/crds/monitoring.coreos.com_podmonitors.yaml \
      -f https://raw.githubusercontent.com/grafana/agent/main/production/operator/crds/monitoring.coreos.com_probes.yaml \
      -f https://raw.githubusercontent.com/grafana/agent/main/production/operator/crds/monitoring.coreos.com_servicemonitors.yaml \
      -f https://raw.githubusercontent.com/grafana/agent/main/production/operator/crds/monitoring.grafana.com_grafanaagents.yaml \
      -f https://raw.githubusercontent.com/grafana/agent/main/production/operator/crds/monitoring.grafana.com_integrations.yaml \
      -f https://raw.githubusercontent.com/grafana/agent/main/production/operator/crds/monitoring.grafana.com_logsinstances.yaml \
      -f https://raw.githubusercontent.com/grafana/agent/main/production/operator/crds/monitoring.grafana.com_metricsinstances.yaml \
      -f https://raw.githubusercontent.com/grafana/agent/main/production/operator/crds/monitoring.grafana.com_podlogs.yaml
    kubectl apply -f grafana-agent-operator.yaml
    kubectl apply -f kube-state-metrics.yaml
    kubectl apply -f grafana-agent.yaml
    kubectl apply -f custom-resource-metrics.yaml
    kubectl apply -f custom-resource-logs.yaml
    kubectl apply -f event-handler.yaml
    kubectl apply -f custom-resource-cost-metrics.yaml
    ```
