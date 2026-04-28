# Observability Stack

## Purpose

The observability stack provides metrics collection and visualisation for the Kubernetes cluster.

## Components

Current components:

- Grafana
- VictoriaMetrics
- vmagent
- kube-state-metrics

## Deployment Style

Most observability components are deployed using Flux-managed HelmRelease resources.

## Current Flow

kube-state-metrics
    ->
vmagent
    ->
VictoriaMetrics
    ->
Grafana

## Notes

The current stack intentionally avoids deploying the full Prometheus stack in order to better understand the individual components and data flow.

The platform currently focuses on learning and operational understanding rather than maximum automation.
