# Case study — homelab-stacks (operable Compose stacks)

## TL;DR
`homelab-stacks` is a production-inspired homelab repo focused on **day-2 operability**: repeatable Docker Compose stacks, clear runtime boundaries, makefile-first operations, actionable monitoring (metrics/logs/alerts/runbooks), and recovery posture (backup/restore guidance and tooling).

Outcome: consistent runtime boundaries with **day-2 entrypoints** for lifecycle, validation, observability, and recovery.

This case study explains the problem I was solving, the design decisions I made, and where to verify the implementation.

---

## Context
Homelabs often drift into host-specific setups: hard-coded paths, undocumented procedures, and stacks that are easy to start but harder to operate over time (upgrades, troubleshooting, backups/restores, and incident response).

I wanted a repo that works as an operations-ready reference: **predictable entrypoints, explicit contracts, and evidence that it can be operated**, not just deployed.

## What you can verify (evidence)
- Runtime contract: [docs/contract.md][hs-contract] (runtime boundaries, overrides and templates).
- Monitoring entrypoint: [stacks/monitoring/README.md][hs-monitoring-readme] (dashboards, alerting, runbooks).
- Runbooks: [stacks/monitoring/runbooks/][hs-runbooks] (linked from alerts via `runbook_url` for fast triage).
- Backup/restore: [ops/backups/README.md][hs-backups] (Restic-based workflows and recovery steps).
- Ops entrypoint: [Makefile][hs-makefile] (validation and stack lifecycle targets).

## Goals
- **Portability**: define a stable runtime contract (paths, overrides, templates) to avoid host-specific assumptions and keep stacks reproducible across environments.
- **Day-2 operations first**: ensure common operational tasks are one command away (status, lifecycle, validation, backups, restore checks).
- **Actionable observability**: tie metrics, logs, and alerting to curated dashboards and concrete operator actions via runbooks.
- **Recovery posture**: document and support backup and restore workflows, explicitly encouraging restore verification as part of normal operations.

## Non-goals
- Kubernetes or multi-node orchestration.
- Infinite scalability, performance benchmarking, or capacity planning.
- Enterprise-grade security hardening or compliance-driven controls.
- A generic framework or product intended to fit all use cases.

## Approach (key decisions)
### 1) Define a runtime contract (reproducibility without leaking host details)
I separated **repo content** from **runtime-only configuration** via templates and overrides, so the repo stays shareable while per-host settings live outside it (paths, secrets, host-specific mounts).

**Why it matters**: portability and clean reviews. A clear contract keeps configuration predictable across machines.

### 2) Makefile-first ops: one entrypoint for day-2 workflows
Instead of scattering “random docker compose commands” across READMEs, I concentrated operations into a make-driven workflow: validation, stack lifecycle, health/status checks, and operational tasks.

**Why it matters**: consistent, repeatable operations and fewer manual steps.

### 3) Observability as an operable stack
Monitoring is treated as an operable stack: metrics and logs are wired into dashboards, alert routing, and runbooks. The intent is not “pretty Grafana” but **actionable signal**.

**Why it matters**: dashboards are most useful when paired with alerting and clear operational guidance.

### 4) Backups and restores as first-class operations (Restic)
Backup/restore workflows are documented and operationally visible. In addition to guidance, the portfolio evidence pack includes Restic metrics surfaced in Grafana, reinforcing that recovery posture is part of normal operations.

**Why it matters**: reliable systems include both observability and recovery procedures.

## Tradeoffs (conscious choices)
- **Docker Compose over Kubernetes:** prioritised human reviewability and operational simplicity on a single host over premature scalability; the goal is to understand and operate the system end-to-end before introducing orchestration complexity.
- **Privileged/rootful containers and simplified secrets:** accepted a controlled increase in risk to expose meaningful host and container metrics, with an explicit focus on limiting blast radius rather than pursuing formal security hardening unsuitable for this context.
- **Fewer services and alerts, fully operable:** prioritised stacks that can be monitored, validated, troubleshot, and recovered end-to-end over a broader but partially operable service catalogue.
- **Operational guidance first:** avoided adding features without clear runbooks and operator actions, as undocumented features tend to accumulate faster than the ability to understand or fix them under pressure.
- **Makefile-first workflows:** automated repetitive tasks while keeping execution paths explicit and traceable, favouring debuggability and operator understanding over opaque “one-click” automation.
- **Documented runtime overrides:** enforced a clear separation between public configuration and runtime-only overrides to reduce human error while keeping system behaviour predictable and auditable.
- **No geographic-level DR:** limited disaster recovery to service-level backups and restores; site-level disasters require custody, redundancy and off-site strategies appropriate to more serious environments.

## What’s next
- Expand validation where it reduces operational risk (runtime contract checks, env/template drift, and preflight sanity checks).
- Keep docs and runbooks aligned with operational entrypoints (Makefile targets, recovery steps, and troubleshooting notes).

[hs-contract]: https://github.com/hugomolinfresneda/homelab-stacks/blob/main/docs/contract.md
[hs-monitoring-readme]: https://github.com/hugomolinfresneda/homelab-stacks/blob/main/stacks/monitoring/README.md
[hs-runbooks]: https://github.com/hugomolinfresneda/homelab-stacks/tree/main/stacks/monitoring/runbooks
[hs-backups]: https://github.com/hugomolinfresneda/homelab-stacks/blob/main/ops/backups/README.md
[hs-makefile]: https://github.com/hugomolinfresneda/homelab-stacks/blob/main/Makefile
