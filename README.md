# Flux GitOps Templates

This repository contains a curated catalog of Flux CD templates and Kubernetes manifests designed for rapidly bootstrapping ephemeral Kubernetes clusters and local dev environments for experimentation.

## The GitOps Bootstrap TUI

This template repository is designed to be paired with the **[GitOps Bootstrap TUI](https://github.com/basarsubasi/gitops-tui)**, a fast, interactive terminal user interface built in Rust. 

The TUI allows you to:
- Instantly browse this template catalog in a clean tree explorer.
- Selectively enable or disable specific components (like choosing Postgres over MongoDB, or adding Observability tools).
- Customize default Helm chart values on the fly.
- Automatically generate the final GitOps repository structure.
- Bootstrap Flux CD and spin up a local `git daemon` to synchronize your cluster instantly.

## Current Catalog

The repository is structured around Kustomize `bases/` representing reusable stacks, and `clusters/` (the final generated deployment configurations). 

Here is an overview of the current supported bases in the catalog:

###  Apps
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
