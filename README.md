Homelab Platform

A production-style Kubernetes platform built and operated as a
self-directed Platform / SRE engineering project.

This repository defines and manages a k3s-based Kubernetes environment
using Git as the source of truth. The focus is not on running
applications, but on understanding and operating the platform that runs
them.

The system evolves incrementally, with tooling introduced deliberately
to understand behaviour, trade-offs, and failure modes.

------------------------------------------------------------------------

Platform Overview

Core components currently include:

-   k3s (single-node, evolving toward multi-node)
-   Flux (GitOps reconciliation)
-   Traefik (Ingress)
-   cert-manager (TLS automation)
-   vmagent + kube-state-metrics (metrics pipeline)
-   Grafana (visualisation)
-   Loki (log aggregation, in progress)
-   NFS-backed persistent storage
-   Internal DNS (Pi-hole) with split-DNS via Tailscale

The platform is designed to mirror real-world operational patterns while
remaining intentionally constrained for clarity.

------------------------------------------------------------------------

Design Principles

-   Declarative by default — infrastructure and workloads are
    Git-managed.
-   Reconciliation over manual intervention — drift is corrected
    automatically.
-   Observability first — metrics and logs are treated as core system
    components.
-   Incremental complexity — tools are added only when a problem
    justifies them.
-   Failure as a learning tool — components are intentionally stressed
    or broken to understand behaviour under fault.

The goal is operational depth, not tool accumulation.

------------------------------------------------------------------------

Operational Capabilities

This platform exercises practical SRE concerns including:

-   GitOps-based deployment and drift control
-   Ingress and TLS lifecycle management
-   Persistent volume provisioning and stateful workload management
-   Metrics ingestion and visualisation
-   Log aggregation and query workflows
-   Namespace isolation and configuration separation
-   Upgrade and recovery testing
-   Controlled failure experimentation

Workloads exist primarily as realistic test cases for these operational
concerns.

------------------------------------------------------------------------

Repository Structure

docs/ Architecture notes, design decisions, and failure documentation
k8s/ Kubernetes manifests (infrastructure, platform services, workloads)

As the platform matures, additional automation and validation tooling
will be introduced in a controlled manner.

------------------------------------------------------------------------

Status

Actively evolving.

This repository reflects a living system that changes as new concepts
are learned, tested, and refined. Refactors and structural improvements
are intentional and documented.

------------------------------------------------------------------------

Purpose

This project exists to bridge the gap between:

“I understand the theory”
and
“I have designed, deployed, observed, broken, and recovered this system
myself.”

It is structured to reflect how modern Platform and SRE teams reason
about infrastructure: through declarative state, observability, and
operational discipline.
