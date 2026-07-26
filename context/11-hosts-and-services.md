# Hosts and Services

## Physical Infrastructure

| Host | Role |
|---|---|
| pve1 | Proxmox hypervisor |
| pve2 | Proxmox hypervisor hosting `k3s01v` |

---

## Virtual Machines

| VM | Purpose |
|---|---|
| k3s01v | Single-node Kubernetes cluster |
| fs01v | File and NFS storage server |
| pihole01v | Internal DNS |
| mediaserver01v | Current Docker media-service host |

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

| Application | Kubernetes hostname | Household runtime |
|---|---|---|
| Jellyfin | jellyfin.home.lan | Docker; Kubernetes cutover planned |
| Sonarr | sonarr.home.lan | Docker; Kubernetes cutover planned |
| Radarr | radarr.home.lan | Docker; Kubernetes cutover planned |
| SABnzbd | sabnzbd.home.lan | Docker; Kubernetes cutover planned |
| Grafana | grafana.home.lan | Kubernetes platform |

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
- Docker remains the current household media runtime
