# Kubernetes Design

## Why k3s?

This platform is built on **k3s**, a lightweight Kubernetes distribution
that maintains production API parity while reducing operational
overhead.

k3s was chosen for the following reasons:

-   Single binary distribution
-   Embedded datastore (SQLite initially)
-   Minimal operational complexity
-   Sensible defaults
-   Easy multi-node expansion path
-   Widely used outside large cloud providers

k3s is not a "cut-down Kubernetes". It is upstream Kubernetes with
pragmatic guardrails and reduced bootstrap complexity.

------------------------------------------------------------------------

## Why Not kubeadm / MicroK8s / Docker Desktop?

**kubeadm** - More manual control, but increased operational
complexity - Unnecessary for a constrained homelab environment - Higher
setup and maintenance overhead

**MicroK8s** - Snap-based packaging - Slightly more opaque internal
management - Less transparent for Git-driven lifecycle control

**Docker Desktop** - Designed for local development - Not appropriate
for production-style operation - Limited realism for multi-node
expansion

k3s provides the best balance between realism and operational
simplicity.

------------------------------------------------------------------------

## Deployment Strategy

The cluster began as a single-node deployment to:

-   Minimise initial complexity
-   Focus on core Kubernetes concepts
-   Avoid premature HA patterns
-   Understand control plane behaviour in isolation

The design allows controlled evolution toward multi-node architecture.

------------------------------------------------------------------------

## VM Sizing

Initial sizing is intentionally conservative:

-   CPU: modest allocation suitable for homelab hardware
-   Memory: sufficient for observability stack + workloads
-   Storage: separate persistent NFS-backed volumes

The goal is to observe resource pressure and scaling behaviour rather
than overprovision.

------------------------------------------------------------------------

## Installation

k3s is installed using the official installation method:

``` bash
curl -sfL https://get.k3s.io | sh -
```

Configuration changes are documented and version-controlled where
possible.

------------------------------------------------------------------------

## Current Limitations

-   Single-node control plane
-   Embedded datastore (SQLite)
-   No HA control plane
-   Backup strategy evolving
-   No network segmentation (yet)

These constraints are intentional and reflect staged platform evolution.
