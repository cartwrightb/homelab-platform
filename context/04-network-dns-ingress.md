# Network, DNS, and Ingress

## DNS

Internal domain: `home.lan`

DNS is currently provided by Pi-hole.

## Ingress

Traefik is the ingress controller installed by k3s.

Ingress manifests currently exist under:

`k8s/infra/ingress/`

Current ingress-based services include:

- jellyfin.home.lan
- radarr.home.lan
- sonarr.home.lan
- sabnzbd.home.lan
- grafana.home.lan

## TLS

TLS is managed using cert-manager.

Wildcard certificates are used for the `home.lan` domain.

The wildcard certificate secret is reused across multiple ingress resources.

## Notes

This is an internal-only homelab environment.

The platform currently assumes trusted internal network access.