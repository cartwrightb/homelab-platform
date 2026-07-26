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

The cluster and platform components are operational. The established
household media services still run in Docker on `mediaserver01v`; the
Kubernetes media workloads are a working parallel environment awaiting
controlled cutover.

The private `homelab-knowledge-base` repository is authoritative for current
estate and workload placement. This repository is authoritative for
Kubernetes desired state.
