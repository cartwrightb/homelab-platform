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
