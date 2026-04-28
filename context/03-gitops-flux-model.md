# GitOps and Flux Model

## Overview

Flux reconciles this GitHub repository into the k3s cluster.

The repository is the desired state.

Manual cluster changes should be avoided unless testing or troubleshooting.

## Cluster Entrypoint

The Flux entrypoint is:

`clusters/k3s01v/`

This includes:

- `flux-system/`
- `kustomizations/`
- `kustomization.yaml`

## Flux System

`clusters/k3s01v/flux-system/` contains the Flux bootstrap manifests.

These should not normally be manually edited unless intentionally changing the Flux bootstrap configuration.

## Root Kustomizations

The main Flux Kustomization resources are under:

`clusters/k3s01v/kustomizations/`

Current root areas:

- infra
- media
- ops

These point Flux at the matching platform areas under `k8s/`.

## Reconciliation Model

Expected flow:

GitHub repo
    ->
Flux source-controller
    ->
Flux kustomize-controller
    ->
clusters/k3s01v/kustomizations/
    ->
k8s/infra
k8s/media
k8s/ops

## Ordering

Infrastructure should reconcile before applications.

Expected dependency direction:

infra
    ->
media
infra
    ->
ops

Applications should not assume cert-manager, namespaces, TLS, ingress, or storage exist unless infra has reconciled successfully.

## Working Rules

When adding or changing platform components:

- update the relevant folder under `k8s/`
- update that folder’s `kustomization.yaml`
- ensure the area is included in the relevant Flux Kustomization
- avoid direct manual changes to the live cluster
- use Flux status commands to verify reconciliation

Useful checks:

- flux get sources git -A
- flux get kustomizations -A
- flux get helmreleases -A
- kubectl get kustomizations.kustomize.toolkit.fluxcd.io -A