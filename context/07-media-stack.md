# Media Stack

## Applications

Current media applications:

- Jellyfin
- Radarr
- Sonarr
- SABnzbd

## Deployment Style

Media apps are currently deployed using standard Kubernetes manifests rather than Helm charts.

Each application typically contains:

- deployment.yaml
- service.yaml
- pvc-config.yaml
- kustomization.yaml

## Networking

Ingress resources are centralised under:

`k8s/infra/ingress/`

## Storage

Applications use persistent volumes for configuration data.

Shared media storage is provided separately through the infrastructure storage layer.

## Notes

The media stack is intentionally simple to support learning Kubernetes fundamentals before abstracting everything behind Helm charts.

These Kubernetes workloads are built and working, but they have not replaced
the established Docker instances that currently serve the household. Future
cutover must be performed one service at a time with verified backup,
validation, and rollback.
