# Homelab Platform

This repository documents and manages my personal homelab platform, built to learn and apply DevOps, Platform Engineering, and Site Reliability Engineering (SRE) practices in a realistic, production-style environment.

The platform evolves incrementally, starting from a single-node Kubernetes cluster and expanding over time to include GitOps workflows, automation, observability, security controls, and reliability patterns.

While the cluster runs real workloads, the primary purpose of this project is learning, experimentation, and documentation of modern infrastructure practices.

---

## Goals

- Build hands-on Kubernetes experience using real services
- Practice Git-based workflows and declarative infrastructure
- Apply SRE principles such as:
  - Declarative configuration
  - Drift control
  - Automation over click-ops
  - Incremental platform evolution
- Develop a portfolio-quality project aligned with modern SRE / Platform roles

---

## Scope & Philosophy

This homelab is treated as a miniature production environment, not a toy setup:

- Everything is documented and version-controlled
- Manual changes are avoided in favour of Git-managed state
- Failures are treated as learning opportunities
- Complexity is introduced deliberately and incrementally

The emphasis is on how the platform is built and operated — not the specific applications running on it.

---

## Workloads

The cluster currently hosts a mix of infrastructure components and application workloads, including media-related services.

These workloads are used purely as realistic, stateful Kubernetes examples to explore:

- Persistent storage (NFS, PVCs, provisioning)
- Ingress and TLS (Traefik, cert-manager)
- Namespace isolation
- Secrets and configuration management
- Upgrade and recovery workflows

They are not the focus of the project — the platform itself is.

---

## Legal & Usage Notice

IMPORTANT

This homelab is used strictly for legal purposes only.

- All media managed or consumed through this platform is:
  - Personally owned, or
  - Freely and legally obtained, or
  - Used for testing and demonstration purposes only
- No copyrighted material is distributed, shared, or accessed unlawfully

This project exists solely to demonstrate technical infrastructure design and operational practices, not content acquisition.

---

## Repository Structure

docs/        # Architecture notes, design decisions, and learning documentation
k8s/         # Kubernetes manifests (infra, platform services, workloads)

Additional structure and tooling (GitOps, CI/CD, validation, etc.) will be introduced as the platform matures.

---

## Status

Actively evolving

This repository reflects a living system that changes as new concepts are learned and applied.
Expect refactors, restructuring, and iterative improvements over time.

---

## Why This Exists

This project exists to bridge the gap between:

“I understand the theory”
and
“I have built and operated this myself”

It is intentionally designed to mirror how modern SRE and Platform teams think, work, and evolve systems.
