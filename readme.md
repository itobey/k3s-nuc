# K3s on an Intel NUC

This repository contains the GitOps configuration for my single-node K3s cluster on an Intel NUC. Argo CD deploys
Kubernetes manifests and Helm charts. The repository also contains encrypted credentials managed by Sealed Secrets.

## Repository layout

- [`deploy/argo/`](deploy/argo/) contains the Argo CD Application definitions, including applications that use external
  Helm charts.
- [`deploy/`](deploy/) contains the application manifests and local Helm charts.
- [`ingress-route-argo.yaml`](ingress-route-argo.yaml) defines the Traefik route for Argo CD.

## Applications

| Application                                                     | Area                   | Purpose                                                           |
|-----------------------------------------------------------------|------------------------|-------------------------------------------------------------------|
| [Baïkal](deploy/argo/baikal.yaml)                               | Personal services      | CalDAV calendars and CardDAV contacts                             |
| [cert-manager](deploy/argo/cert-manager.yaml)                   | Cluster infrastructure | Issues and renews TLS certificates                                |
| [Datadog](deploy/argo/datadog.yaml)                             | Observability          | Datadog agent for cluster monitoring                              |
| [Datadog API Collector](deploy/argo/datadog-api-collector.yaml) | Observability          | Collects data from the Datadog API                                |
| [FDDB Exporter](deploy/argo/fddb-exporter.yaml)                 | Observability          | Exports FDDB nutrition data                                       |
| [Gitea](deploy/argo/gitea.yaml)                                 | Development            | Self-hosted Git repositories                                      |
| [Grafana](deploy/argo/grafana.yaml)                             | Observability          | Dashboards for metrics and other data                             |
| [HASS Screenshot](deploy/argo/hass-screenshot.yaml)             | Smart home             | Captures and serves Home Assistant screenshots                    |
| [Headlamp](deploy/argo/headlamp.yaml)                           | Cluster infrastructure | Web UI for inspecting Kubernetes resources                        |
| [Healthchecks](deploy/argo/healthchecks.yaml)                   | Observability          | Monitors scheduled jobs via check-ins                             |
| [Hermes](deploy/argo/hermes.yaml)                               | Automation             | Hermes Agent instance                                             |
| [Hermes Frontier](deploy/argo/hermes-frontier.yaml)             | Automation             | Separate Hermes Agent instance                                    |
| [Home Assistant](deploy/argo/home-assistant.yaml)               | Smart home             | Central control and automation for smart-home devices             |
| [Homer](deploy/argo/homer.yaml)                                 | Personal services      | Start page for self-hosted services                               |
| [InfluxDB 2](deploy/argo/influxdb2.yaml)                        | Databases              | Time-series database                                              |
| [Infrastructure](deploy/argo/infra.yaml)                        | Cluster infrastructure | Shared Traefik middleware and TLS configuration                   |
| [Kasa Exporter](deploy/argo/kasa.yaml)                          | Observability          | Exposes metrics from TP-Link Kasa smart plugs                     |
| [MongoDB](deploy/argo/mongodb.yaml)                             | Databases              | Document database                                                 |
| [Mosquitto](deploy/argo/mosquitto.yaml)                         | Smart home             | MQTT broker with a companion Telegraf deployment                  |
| [Music Assistant](deploy/argo/music-assistant.yaml)             | Media                  | Manages music libraries and playback                              |
| [n8n](deploy/argo/n8n.yaml)                                     | Automation             | Workflow automation                                               |
| [Paperless-ngx](deploy/argo/paperless.yaml)                     | Personal services      | Document archive with OCR                                         |
| [Pi-hole](deploy/argo/pihole.yaml)                              | Networking             | DNS-based filtering                                               |
| [Playlist Mirror](deploy/argo/playlist-mirror.yaml)             | Media                  | Mirrors music playlists                                           |
| [PostgreSQL](deploy/argo/misc.yaml)                             | Databases              | Relational database deployed by the `misc` Application            |
| [Prometheus](deploy/argo/prometheus.yaml)                       | Observability          | Kubernetes metrics collection via kube-prometheus-stack           |
| [Remember This](deploy/argo/remember-this.yaml)                 | Personal services      | Web reader for Amor Fati entries                                  |
| [Resilio Sync](deploy/argo/resilio.yaml)                        | Personal services      | Peer-to-peer file synchronization                                 |
| [Sealed Secrets](deploy/argo/sealed-secrets.yaml)               | Cluster infrastructure | Converts encrypted SealedSecret resources into Kubernetes Secrets |
| [SearXNG](deploy/argo/searxng.yaml)                             | Personal services      | Self-hosted metasearch engine                                     |
| [Stuff Control](deploy/argo/stuff-control.yaml)                 | Personal services      | Self-hosted Stuff Control service                                 |
| [Telegraf FRITZ!Box](deploy/argo/telegraf-fritzbox.yaml)        | Observability          | Collects FRITZ!Box metrics                                        |
| [WireGuard](deploy/argo/wireguard.yaml)                         | Networking             | VPN access                                                        |
| [Zigbee2MQTT](deploy/argo/zigbee2mqtt.yaml)                     | Smart home             | Bridges Zigbee devices to MQTT                                    |
| [Z-Wave JS UI](deploy/argo/zwave.yaml)                          | Smart home             | Manages Z-Wave devices and their controller                       |
