# Observability Design

## Goals

Observability within this platform is designed to answer three core questions:

- What is the current state of the cluster?
- What changed when something broke?
- Where should I look first during an incident?

The focus is on building an understandable metrics pipeline before introducing advanced tooling.

---

## Current State

The observability stack is deployed in the `ops` namespace and currently includes:

- VictoriaMetrics (metrics storage backend)
- vmagent (scraping and forwarding metrics)
- kube-state-metrics (Kubernetes object state metrics)
- Grafana (visualisation)

The metrics pipeline is functional and verified end-to-end.

---

## Metrics Architecture

Current metrics flow:

Exporters  
→ vmagent  
→ VictoriaMetrics  
→ Grafana  

### Exporters

- kube-state-metrics provides object-level visibility:
  - Pod status
  - Deployments
  - Replica counts
  - Restarts

Node-level metrics via node-exporter are not yet deployed.

---

## What Can Be Observed Today

With the current setup, the platform can observe:

- Pod lifecycle state
- Restart counts
- Replica drift
- Basic workload health
- Metrics ingestion success

This provides cluster-level visibility but limited host-level visibility.

---

## Known Gaps

- No node-exporter (host CPU, memory, disk metrics unavailable)
- No alerting configured
- No log aggregation yet
- Single-node cluster limits failure modelling
- No long-term retention tuning

These gaps are intentional and reflect staged implementation.

---

## Planned Evolution

### Node-Level Metrics
Deploy node-exporter as a DaemonSet to collect:

- CPU utilisation
- Memory pressure
- Disk usage
- Filesystem metrics

### Log Aggregation
Introduce Loki with a DaemonSet-based log collector to:

- Query logs across namespaces
- Correlate logs with metrics
- Support basic incident investigation workflows

### Alerting
Introduce alert rules for:

- Node resource pressure
- Pod restart thresholds
- Scrape failures
- Certificate expiry

Alerting will follow once metrics and logs are stable.

---

## Philosophy

Observability is being built deliberately and incrementally.

The priority is understanding the data flow and failure behaviour of the pipeline itself before layering alerting complexity on top.
