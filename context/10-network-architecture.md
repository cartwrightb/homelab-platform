# Network Architecture

## Overview

This homelab environment is designed for learning and operating platform engineering technologies including:

- Kubernetes
- GitOps
- observability
- ingress/TLS
- storage
- Linux administration
- automation

The environment is internal-only and not internet-facing.

The Kubernetes cluster currently runs as a single-node k3s VM hosted on Proxmox.

---

## Core Infrastructure

### Proxmox

Proxmox is the virtualization platform hosting the environment.

Current important VMs include:

- k3s01v
- omv01
- pihole01

---

## Kubernetes

Current cluster:

- Distribution: k3s
- Node count: 1
- Node name: k3s01v
- OS: Ubuntu Server

The cluster is managed using Flux GitOps.

---

## DNS

Pi-hole provides internal DNS for the `home.lan` domain.

Examples:

- grafana.home.lan
- jellyfin.home.lan
- sonarr.home.lan
- radarr.home.lan
- sabnzbd.home.lan

---

## Ingress

Traefik is the ingress controller installed by k3s.

Ingress traffic flow:

Client
  ->
Pi-hole DNS
  ->
Traefik
  ->
Kubernetes Service
  ->
Pod

---

## TLS

cert-manager provides internal PKI.

The environment currently uses:

- self-signed root CA
- internal CA issuer
- wildcard certificates for `*.home.lan`

---

## Storage

OMV provides NFS exports used by Kubernetes.

Current storage split:

- media storage
  - shared media content
- appdata storage
  - Kubernetes application configs and persistent data

---

## GitOps

GitHub is the source of truth for the cluster.

Flux reconciles the repository into the cluster.

Repository:

- homelab-platform

---

## Observability

Current observability stack:

- Grafana
- VictoriaMetrics
- vmagent
- kube-state-metrics

Metrics flow:

kube-state-metrics
  ->
vmagent
  ->
VictoriaMetrics
  ->
Grafana

---

## Current Design Philosophy

The environment prioritises:

- simplicity
- operational understanding
- GitOps workflows
- learning Kubernetes fundamentals
- avoiding unnecessary abstraction

The platform intentionally avoids enterprise-scale complexity unless there is a learning or operational reason.