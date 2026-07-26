# Cluster State

## Cluster

- Cluster name/context: k3s01v
- Kubernetes distribution: k3s
- Cluster type: single-node homelab cluster
- Platform: Ubuntu VM running on Proxmox

## Core Components

Current core components include:

- k3s
- Traefik
- Flux
- cert-manager
- local-path storage
- NFS-backed storage

## Namespaces

Known namespaces include:

- flux-system
- cert-manager
- media
- ops

## Important Note

Do not assume live cluster state from this file alone.

Do not interpret a workload represented or deployed here as proof that it is
the active household service. The established media services currently remain
on Docker; consult the private knowledge base for current workload placement.

If current state matters, check using:

- kubectl get nodes
- kubectl get ns
- kubectl get pods -A
- flux get kustomizations -A
- flux get helmreleases -A
