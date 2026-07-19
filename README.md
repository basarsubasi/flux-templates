# Flux GitOps Templates

This repository contains a curated catalog of Flux CD templates and Kubernetes manifests designed for rapidly bootstrapping ephemeral Kubernetes clusters and local dev environments for experimentation.

## The GitOps Bootstrap TUI

This template repository is designed to be paired with the **[GitOps Bootstrap TUI](https://github.com/basarsubasi/gitops-tui)**, a fast, interactive terminal user interface built in Rust. 

The TUI allows you to:
- Instantly browse this template catalog in a clean tree explorer.
- Selectively enable or disable specific components (like choosing Postgres over MongoDB, or adding Observability tools).
- **Component Rules Engine:** The TUI parses `bases/rules.yaml` in this repository to automatically enforce component dependencies (e.g., Database CRs auto-selecting their Operators) and mutual exclusivity (e.g., blocking `grafana` if `victoria-metrics` is selected).
- Customize default Helm chart values on the fly.
- Automatically generate the final GitOps repository structure as a flat, monolithic Kustomize build.
- **Global Deduplication:** The TUI dynamically parses the required namespaces and `HelmRepository` definitions from your selected templates, strips duplicates, and hoists them to a global layer to absolutely prevent Kustomize resource ID collisions.
- Bootstrap Flux CD securely using standard Git provider integrations.

## Current Catalog

Here is an overview of the current supported bases in the catalog:

## Directory Structure
```text
.
├── bases/
│   ├── repositories/       # Centralized HelmRepository definitions
│   ├── infrastructure/     # Core platform controllers, networking, security
│   ├── databases/          # Data stores and caching solutions
│   └── apps/               # Example applications and workloads
└── clusters/
    └── example-cluster-01/ # Pre-configured example of a fully generated cluster
```

### Repositories (Centralized)
- Centralized `HelmRepository` declarations for all components below (Deduplicated automatically to prevent Kustomize build collisions).

### Apps
- **Grafana Quickpizza**: A demo microservices application for Grafana observability.
- **OpenTelemetry Demo**: The official OpenTelemetry astronomy shop demo app.

### Databases
- ClickHouse
- CockroachDB
- Elasticsearch
- Kafka
- MongoDB
- PostgreSQL
- Redis

### Infrastructure

** Controllers & Operators:**
- ClickHouse Operator
- Cockroach Operator
- Elastic Operator
- KEDA (Kubernetes Event-driven Autoscaling)
- MongoDB Operator
- OpenTelemetry Operator
- Postgres Operator
- Strimzi Kafka Operator

**Networking:**
- Cilium
- Consul
- Istio

**Observability:**
- Alertmanager
- Elasticsearch
- Filebeat
- Grafana
- Jaeger
- Kibana
- Kube-Prometheus-Stack
- Logstash
- Loki
- Mimir
- OpenTelemetry Collector / OBI
- Prometheus
- Promtail
- Tempo
- Victoria Metrics K8s Stack

**Security:**
- Cert-Manager
- Tetragon
- Vault

**Storage:**
- Rook-Ceph

**UI & Dashboards:**
- Backstage
- Headlamp
- KExp
- Redpanda Console

## Usage Structure

When generating a cluster (e.g. via the TUI), the tool will extract components from the `bases/` directory and structure them in the `clusters/` folder. Flux CD is then pointed at your cluster's specific path to begin automated reconciliation.
