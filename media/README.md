# Media (screenshots + architecture)

This folder contains sanitized evidence used by the portfolio README: dashboards, one alert example, and a high-level architecture diagram.

## Quick review (30–60s)
1. Open the Grafana dashboards (homelab: host/containers/backups; demo: blackbox targets + logs).
2. Open [alert-example.png](alert-example.png) to see an actionable alert with labels/annotations and a runbook link.
3. Open [architecture-diagram.png](architecture-diagram.png) for the level-1 system overview (or [.mmd](architecture-diagram.mmd) for online rendering).

## Contents
- [grafana-host-overview.png](grafana-host-overview.png) — host-level signals (CPU/memory/disk/network) for infra baseline.
- [grafana-containers-overview.png](grafana-containers-overview.png) — container-level signals (resource usage, restarts, top offenders).
- [grafana-backups-overview.png](grafana-backups-overview.png) — backup posture (freshness, success/failures, duration, delta).
- [grafana-demo-blackbox-targets.png](grafana-demo-blackbox-targets.png) — demo blackbox targets lifecycle (add/remove) with visible Prometheus reload + embedded runbook.
- [grafana-demo-logs-logspammer.png](grafana-demo-logs-logspammer.png) — demo Loki logs filtered to the log generator (ingestion sanity check; isolated).
- [alert-example.png](alert-example.png) — alert example showing labels/annotations, severity and a runbook link (actionable triage).
- [architecture-diagram.mmd](architecture-diagram.mmd) — Mermaid source for the level-1 architecture diagram.
- [architecture-diagram.svg](architecture-diagram.svg) — rendered diagram (preferred for readability).
- [architecture-diagram.png](architecture-diagram.png) — rendered diagram (preview-friendly).

## Notes
- Screenshots are sanitized: hostnames, domains, IPs, paths, tokens and personal identifiers have been redacted.
- `grafana-demo-*` screenshots come from the reproducible monitoring demo mode.
- Images are illustrative and intended to show operational patterns and review entrypoints.
