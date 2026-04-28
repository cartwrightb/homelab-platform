# Platform Overview

This repository manages my homelab Kubernetes platform.

The platform is a single-node k3s cluster running as a VM on Proxmox.

Flux is used for GitOps. The GitHub repository is the desired state for the cluster.

The current major platform areas are:

- Infrastructure:
  - namespaces
  - storage
  - cert-manager
  - TLS
  - ingress

- Media applications:
  - Jellyfin
  - Radarr
  - Sonarr
  - SABnzbd

- Operations:
  - Grafana
  - VictoriaMetrics
  - vmagent
  - kube-state-metrics

The purpose of the platform is both practical homelab hosting and learning production-style Kubernetes/GitOps patterns.

