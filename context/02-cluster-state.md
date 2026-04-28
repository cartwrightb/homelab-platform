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

If current state matters, check using:

- kubectl get nodes
- kubectl get ns
- kubectl get pods -A
- flux get kustomizations -A
- flux get helmreleases -A

