# AGENTS.md

This repository is the source of truth for my homelab Kubernetes platform.

## Purpose

This repo manages a single-node k3s homelab cluster using Flux GitOps.

The goal is to learn and operate Kubernetes properly, including GitOps, ingress, TLS, storage, observability, and application deployment.

## Cluster

- Cluster name/context: k3s01v
- Kubernetes distribution: k3s
- GitOps controller: Flux
- Ingress controller: Traefik from k3s
- Internal DNS domain: home.lan
- TLS: cert-manager with internal/self-signed CA
- Main namespaces:
  - media
  - ops
  - cert-manager
  - flux-system

## Repository Layout

- `clusters/k3s01v/`
  - Flux cluster entrypoint.
  - Contains `flux-system/` and root Flux Kustomizations.
- `clusters/k3s01v/kustomizations/`
  - Defines Flux reconciliation for infra, media, and ops.
- `k8s/infra/`
  - Shared platform infrastructure: namespaces, cert-manager, TLS, ingress, storage.
- `k8s/media/`
  - Media applications: Jellyfin, Radarr, Sonarr, SABnzbd.
- `k8s/ops/`
  - Operational tooling, currently observability.
- `k8s/ops/observability/`
  - Grafana, VictoriaMetrics, vmagent, kube-state-metrics, Helm repositories, ingress, TLS.
- `docs/`
  - Human-facing design documentation.
- `context/`
  - Agent-facing operational context for Codex/ChatGPT.

## Working Rules for Agents

- Do not invent live cluster state.
- If live state matters, ask for `kubectl` or `flux` output.
- Prefer GitOps changes over manual `kubectl apply`.
- Follow the existing repo layout and naming conventions.
- Keep manifests simple and understandable.
- Explain proposed changes before making them.
- Do not create or modify real secrets, passwords, tokens, or private keys.
- Do not commit generated manifests, rendered Helm output, or downloaded charts unless explicitly required.
- When adding a new component, wire it into the correct `kustomization.yaml`.
- When adding a new Flux-managed area, ensure it is referenced from `clusters/k3s01v/kustomizations/`.
- Prefer small, reviewable changes.

## Learning and Teaching Style

This repository is also a learning platform.

The operator prefers:
- understanding systems deeply
- learning operational behaviour
- understanding data flow and dependencies
- simple and explicit configurations
- incremental improvements
- production-style reasoning without unnecessary complexity

Do not optimise purely for speed or abstraction.

When proposing changes:
- explain why
- explain component interactions
- explain trade-offs
- explain operational impact
- explain Kubernetes behaviour where relevant

Avoid “magic” solutions without explanation.