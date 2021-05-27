# changes
source: https://github.com/cablespaghetti/k3s-monitoring

seine kube-prometheus-stack-values.yaml genommen und in custom-values.yaml geändert
- ~~dort nur grafana disabled~~

Die Basis davon ist: https://github.com/prometheus-community/helm-charts/tree/main/charts/kube-prometheus-stack
Habe das als Basis für das Chart genommen und die Version von dem Dude exportiert, die er angibt:
helm pull prometheus-community/kube-prometheus-stack --version 13.4.1 --untar 
