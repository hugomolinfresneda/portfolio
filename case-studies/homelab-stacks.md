# Case study — homelab-stacks (operable Compose stacks)

## TL;DR
`homelab-stacks` is a production-inspired homelab repo focused on **day-2 operability**: repeatable Docker Compose stacks, clear runtime boundaries, makefile-first operations, actionable monitoring (metrics/logs/alerts/runbooks), and recovery posture (backup/restore guidance and tooling).

Outcome: consistent runtime boundaries with **day-2 entrypoints** for lifecycle, validation, observability, and recovery.

This case study explains the problem I was solving, the design decisions I made, and where to verify the implementation.

---

## Context
Homelabs often drift into host-specific setups: hard-coded paths, undocumented procedures, and stacks that are easy to start but harder to operate over time (upgrades, troubleshooting, backups/restores, and incident response).

I wanted a repo that works as an operations-ready reference: **predictable entrypoints, explicit contracts, and evidence that it can be operated**, not just deployed.

## Goals
- **Portability**: avoid host-specific assumptions by defining a stable runtime contract (paths, overrides, templates).
- **Day-2 operations first**: common tasks should be one command away (status, lifecycle, validation, backups, restore checks).
- **Actionable observability**: metrics + logs + alerting tied to dashboards and runbooks.
- **Recovery posture**: document and support backup/restore workflows (and encourage restore testing).

## Non-goals
- Not aiming for Kubernetes or “infinite scalability”.
- Not trying to be a generic framework for everyone; this is a focused, reviewable portfolio artifact.
- Not a full security hardening reference (only pragmatic guardrails where they improve operability).

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

## What you can verify (evidence)
- Runtime contract: [docs/contract.md][hs-contract] (runtime boundaries, overrides and templates).
- Monitoring entrypoint: [stacks/monitoring/README.md][hs-monitoring-readme] (dashboards, alerting, runbooks).
- Runbooks: [stacks/monitoring/runbooks/][hs-runbooks] (linked from alerts via `runbook_url` for fast triage).
- Backup/restore: [ops/backups/README.md][hs-backups] (Restic-based workflows and recovery steps).
- Ops entrypoint: [Makefile][hs-makefile] (validation and stack lifecycle targets).

## Tradeoffs (conscious choices)
- **Docker Compose over orchestration**: chosen for reviewability and operational simplicity in a homelab context.
- **Pragmatism over purity**: some components may require rootful Docker or privileged visibility to expose meaningful host/container metrics (explicitly treated as a tradeoff, not an accident).
- **Operational completeness over catalog size**: prioritised stacks that are fully operable (docs, validation, monitoring, recovery) over maximising the number of services included.

## What’s next
- Expand validation where it reduces operational risk (runtime contract checks, env/template drift, and preflight sanity checks).
- Add an interview-ready walkthrough that covers backup + restore verification and alert triage end-to-end.
- Keep docs and runbooks aligned with operational entrypoints (Makefile targets, recovery steps, and troubleshooting notes).


[hs-contract]: https://github.com/hugomolinfresneda/homelab-stacks/blob/main/docs/contract.md
[hs-monitoring-readme]: https://github.com/hugomolinfresneda/homelab-stacks/blob/main/stacks/monitoring/README.md
[hs-runbooks]: https://github.com/hugomolinfresneda/homelab-stacks/tree/main/stacks/monitoring/runbooks
[hs-backups]: https://github.com/hugomolinfresneda/homelab-stacks/blob/main/ops/backups/README.md
[hs-makefile]: https://github.com/hugomolinfresneda/homelab-stacks/blob/main/Makefile
