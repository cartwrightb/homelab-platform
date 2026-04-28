# Repository Map

This repo is organised around Flux GitOps.

## clusters/k3s01v

This is the cluster entrypoint.

clusters/k3s01v/
├── flux-system/
├── kustomizations/
└── kustomization.yaml

`flux-system/` contains the Flux bootstrap manifests.

`kustomizations/` contains Flux Kustomization resources for major platform areas:

- infra.yaml
- media.yaml
- ops.yaml

These point Flux at the relevant folders under `k8s/`.

## k8s/infra

Shared platform infrastructure.

Current areas:

- cert-manager/
- ingress/
- namespaces/
- storage/
- tls/

This layer should be reconciled before applications because apps depend on namespaces, storage, ingress, and TLS.

## k8s/media

Media application workloads.

Current apps:

- Jellyfin
- Radarr
- Sonarr
- SABnzbd

These are currently defined using plain Kubernetes manifests rather than HelmRelease.

Each app generally has:

- deployment.yaml
- service.yaml
- pvc-config.yaml
- kustomization.yaml

Ingress for these apps currently lives under `k8s/infra/ingress`.

## k8s/ops

Operational tooling.

Current area:

- observability/

## k8s/ops/observability

Observability stack.

Current components:

- Grafana
- VictoriaMetrics
- vmagent
- kube-state-metrics
- HelmRepository definitions
- Grafana ingress
- TLS certificate manifest

Most observability components are HelmRelease-based.

## docs

Human-facing design documentation.

Current docs:

- kubernetes-design.md
- networking-dns.md
- observability.md
- storage-design.md

## context

Agent-facing operational context.

This folder should explain the actual system, decisions, assumptions, and rules so Codex can work safely in the repo.
