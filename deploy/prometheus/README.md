# changes
source: https://github.com/cablespaghetti/k3s-monitoring

moved kube-prometheus-stack-values.yaml to custom-values.yaml
- ~~enabled grafana~~
- added scrape config for kasa

based on: https://github.com/prometheus-community/helm-charts/tree/main/charts/kube-prometheus-stack
Used this for an export:
helm pull prometheus-community/kube-prometheus-stack --version 13.4.1 --untar 
