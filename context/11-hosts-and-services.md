# Hosts and Services

## Physical Infrastructure

| Host | Role |
|---|---|
| proxmox01 | Main Proxmox hypervisor |

---

## Virtual Machines

| VM | Purpose |
|---|---|
| k3s01v | Single-node Kubernetes cluster |
| omv01 | NFS storage server |
| pihole01 | Internal DNS |

---

## Kubernetes Platform Services

| Service | Purpose |
|---|---|
| Flux | GitOps reconciliation |
| Traefik | Ingress controller |
| cert-manager | Internal PKI and certificates |
| VictoriaMetrics | Metrics storage |
| vmagent | Metrics scraping/forwarding |
| Grafana | Metrics visualisation |
| kube-state-metrics | Kubernetes metrics exporter |

---

## Media Applications

| Application | Hostname |
|---|---|
| Jellyfin | jellyfin.home.lan |
| Sonarr | sonarr.home.lan |
| Radarr | radarr.home.lan |
| SABnzbd | sabnzbd.home.lan |
| Grafana | grafana.home.lan |

---

## Storage Exports

| Export | Purpose |
|---|---|
| /export/media | Shared media storage |
| /export/k8s-appdata | Kubernetes persistent app data |

---

## Important Relationships

### Flux

Flux reconciles the GitHub repository into the Kubernetes cluster.

### OMV

OMV provides NFS storage consumed by Kubernetes.

### Pi-hole

Pi-hole provides DNS resolution for internal ingress hostnames.

### Traefik

Traefik routes ingress traffic to Kubernetes services.

### cert-manager

cert-manager provides wildcard TLS certificates used by ingress resources.

---

## Current Operational Assumptions

- Internal trusted network
- No public internet exposure
- Single-node Kubernetes
- GitOps-first operational model
- Internal-only PKI