# VictoriaMetric

## k8s stack

```sh
helm repo add grafana https://grafana.github.io/helm-charts
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo add vm https://victoriametrics.github.io/helm-charts/
helm repo update
```

### extract values

```sh
helm search repo vm/victoria-metrics-k8s-stack -l
helm show values vm/victoria-metrics-k8s-stack > values.yaml
```

### install

```sh
kubectl apply -f https://raw.githubusercontent.com/VictoriaMetrics/helm-charts/master/charts/victoria-metrics-k8s-stack/charts/crds/crds/crd.yaml
helm upgrade --install vm-release vm/victoria-metrics-k8s-stack -f values.yaml -n vm-space --debug --dry-run
helm upgrade --install vm-release vm/victoria-metrics-k8s-stack -f values.yaml -n vm-space --create-namespace
kubectl get pods -A | grep 'victoria-metrics'
```
