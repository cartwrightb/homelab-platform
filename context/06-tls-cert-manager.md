# TLS and cert-manager

## cert-manager

cert-manager is deployed as shared cluster infrastructure.

Location:

`k8s/infra/cert-manager/`

## Certificate Flow

Current certificate flow:

1. Self-signed ClusterIssuer
2. Root CA certificate
3. CA-backed ClusterIssuer
4. Wildcard certificates issued from internal CA

## Current Usage

Wildcard certificates are currently used for:

- media applications
- observability applications

## Notes

This is an internal-only PKI design for homelab use.

The goal is to learn and operate proper TLS flows rather than rely on insecure HTTP-only access.
