# Demo script — homelab-stacks (Monitoring demo mode)

Audience: interview / technical review (5–7 minutes)  
Goal: prove reproducibility + day-2 operability (dashboards, controlled change, visible Prometheus reload)

## Why this demo
The monitoring stack includes a **demo mode** designed for quick evaluation on any machine:
- copy + edit one template: `stacks/monitoring/.env.demo.example` → `stacks/monitoring/.env.demo`
- bring everything up with one command (`demo-up`), scoped by `DEMO_PROJECT`

The core story is an operability loop:

**change → apply → observable feedback → runbook-guided operations**

---

## Preflight (operator)
- Pick a unique `DEMO_PROJECT` for the session (avoid collisions).
- Sanitize your terminal/browser: no hostnames, no personal paths, no secrets in history.
- Have a fallback ready: portfolio `media/` screenshots + architecture diagram.
- Ensure the demo stack is already pulled/built if your network is unreliable.

## Host requirements (where you run the demo)
- Linux host with Docker Engine + Docker Compose plugin
- `make` installed
- Demo ports are free (see `stacks/monitoring/.env.demo.example`)

> Run the commands below from the repo root (so `-f stacks/monitoring/Makefile.demo` resolves correctly).

## Setup (copy/paste)

> Do not paste real secrets on screen. Use demo credentials.

```bash
# 1) Clone
git clone https://github.com/hugomolinfresneda/homelab-stacks
cd homelab-stacks

# 2) Demo env: copy template and set demo credentials (and any required vars)
cp -f stacks/monitoring/.env.demo.example stacks/monitoring/.env.demo
$EDITOR stacks/monitoring/.env.demo
```

### Recommended: use a unique DEMO_PROJECT for the session
```bash
export DEMO_PROJECT="mon-demo"
```

Optional sanity check (render combined compose):
```bash
make -f stacks/monitoring/Makefile.demo demo-config DEMO_PROJECT="$DEMO_PROJECT"
```

Optional config validation (promtool/amtool; does not require the demo to be up):
```bash
make -f stacks/monitoring/Makefile.demo demo-check
```

Bring demo up:
```bash
make -f stacks/monitoring/Makefile.demo demo-up DEMO_PROJECT="$DEMO_PROJECT"
```

List services:
```bash
make -f stacks/monitoring/Makefile.demo demo-ps DEMO_PROJECT="$DEMO_PROJECT"
```

Bring demo down (removes volumes/orphans):
```bash
make -f stacks/monitoring/Makefile.demo demo-down DEMO_PROJECT="$DEMO_PROJECT"
```

If the network remains (rare; optional):
```bash
make -f stacks/monitoring/Makefile.demo demo-rm-net DEMO_PROJECT="$DEMO_PROJECT"
```

### ENVFILE note (only when needed)
`Makefile.demo` defaults to `stacks/monitoring/.env.demo`.  
If your demo env file is in a different location, pass `ENVFILE=/path/to/.env.demo` to these targets:
- `demo-config`, `demo-up`, `demo-down`, `demo-ps`, `demo-reload-prom`

Example:
```bash
make -f stacks/monitoring/Makefile.demo demo-up \
  DEMO_PROJECT="$DEMO_PROJECT" ENVFILE="/path/to/.env.demo"
```

---

## Live demo (minute-by-minute)

### 0:00–0:30 — Context
**Say**
- “This repo is built around day-2 operability: runtime contract, Makefile-first ops, actionable observability, and recovery posture.”
- “Monitoring includes a demo mode to make evaluation reproducible.”
- “I’ll show the demo mode, then a controlled change (blackbox target) and how the reload becomes visible in the dashboard.”

**Show**
- Monitoring README for 10–15 seconds, then move on.

---

### 0:30–2:00 — Reproducible demo mode
**Show**
- Template path: `stacks/monitoring/.env.demo.example` → `.env.demo`
- `demo-up` (if not already running), scoped via `DEMO_PROJECT`

**Why**
- A single, repeatable entrypoint reduces reviewer friction and makes the setup easy to evaluate.

---

### 2:00–3:00 — Dashboards overview
**Show**
- Open Grafana locally (URL/port and credentials are defined in `.env.demo`)
- Briefly show the three polished demo dashboards (no deep dive)

**Say**
- “Dashboards are curated to expose actionable signals, not just charts.”

---

### 3:00–5:30 — Blackbox targets lifecycle (core story)
**Show**
- Open the dashboard: **“Demo - Blackbox Targets & Probes”**
- Highlight:
  - **Reload OK - Prometheus**
  - **Last Reload - Prometheus** (time since reload)
  - Targets total / targets UP
  - Per-target table: UP, HTTP status, average latency
  - Runbook panel embedded in the dashboard (“Manage demo Blackbox targets”)

**Say**
- “This dashboard is designed as an operability loop: manage targets through helpers, reload Prometheus, and the reload is visible here.”
- “The runbook is embedded so the procedure lives at the point of use.”

#### Runbook-driven change (terminal)
> Assumes `DEMO_PROJECT` is already set.

```bash
export JOB="blackbox-http"
export TARGET="https://example.org"

# list current targets for the job
make -f stacks/monitoring/Makefile.demo ls-targets-demo \
  JOB="$JOB" DEMO_PROJECT="$DEMO_PROJECT"

# add a target
make -f stacks/monitoring/Makefile.demo add-target-demo \
  JOB="$JOB" TARGET="$TARGET" DEMO_PROJECT="$DEMO_PROJECT"

# apply changes (reload Prometheus demo)
make -f stacks/monitoring/Makefile.demo demo-reload-prom \
  DEMO_PROJECT="$DEMO_PROJECT" ENVFILE="stacks/monitoring/.env.demo"
```

**Verify in Grafana**
- “Last Reload - Prometheus” updates (reload becomes visible).
- Target appears in the per-target table and counts update after the next scrape.

(Optional, if time allows)
```bash
# remove the target
make -f stacks/monitoring/Makefile.demo rm-target-demo \
  JOB="$JOB" TARGET="$TARGET" DEMO_PROJECT="$DEMO_PROJECT"

# apply removal (reload again)
make -f stacks/monitoring/Makefile.demo demo-reload-prom \
  DEMO_PROJECT="$DEMO_PROJECT" ENVFILE="stacks/monitoring/.env.demo"
```

**Why**
- Controlled change management + visible application of config changes + runbook-guided operations.

> Note: in this sequence, `ENVFILE` is only required for `demo-reload-prom`.  
> If your env file is not `stacks/monitoring/.env.demo`, replace `ENVFILE=...` accordingly.

---

### 5:30–6:30 — Tie-in: runbooks + recovery posture
**Say**
- “Dashboards are paired with runbooks, and the repo documents backup/restore posture (Restic).”

**Show**
- Runbooks directory (briefly)
- Backups README entrypoint (briefly)

---

### 6:30–7:00 — Close
**Say**
- “The focus is operability: predictable entrypoints, actionable signal, and procedures that make changes and recovery verifiable.”

---

### Post-demo (optional)
If you want to clean up immediately after the walkthrough:
> If your env file is not `stacks/monitoring/.env.demo`, replace `ENVFILE=...` accordingly.

```bash
make -f stacks/monitoring/Makefile.demo demo-down \
  DEMO_PROJECT="$DEMO_PROJECT" ENVFILE="stacks/monitoring/.env.demo"

# optional, if the network remains
make -f stacks/monitoring/Makefile.demo demo-rm-net DEMO_PROJECT="$DEMO_PROJECT"
```

---

## Fallback (if live demo fails)
If Docker/Grafana is not available, use the portfolio evidence pack (sanitized screenshots):
> Paths below assume this file lives in `demos/` and `media/` is at repo root.

1) Architecture overview (level 1)
- [media/architecture-diagram.svg](../media/architecture-diagram.svg) (or [.mmd](../media/architecture-diagram.mmd) for online rendering)

2) Dashboards (homelab)
- [media/grafana-host-overview.png](../media/grafana-host-overview.png)
- [media/grafana-containers-overview.png](../media/grafana-containers-overview.png)
- [media/grafana-backups-overview.png](../media/grafana-backups-overview.png)

3) Alert example (actionable triage)
- [media/alert-example.png](../media/alert-example.png) (labels/annotations + severity + runbook link)

4) Core operability loop (demo)
- [media/grafana-demo-blackbox-targets.png](../media/grafana-demo-blackbox-targets.png)  
  Narrate: **change → apply (reload) → observable feedback → runbook-guided ops**  
  Point out: targets count/table + “Last Reload - Prometheus” updating + embedded runbook.

5) Logs ingestion sanity check (demo, optional)
- [media/grafana-demo-logs-logspammer.png](../media/grafana-demo-logs-logspammer.png) (isolated demo logs; shows Loki ingestion + query workflow)

---

## Reference: demo entrypoints
Quick reminder of the targets used in this walkthrough.

```text
demo-config           - Render combined compose (sanity check)
demo-up               - Bring demo up (project-scoped via DEMO_PROJECT)
demo-down             - Bring demo down (removes volumes + orphans)
demo-ps               - List demo services
demo-reload-prom      - SIGHUP Prometheus to reload config
demo-check            - promtool/amtool validation of demo configs
demo-rm-net           - Remove demo network if it remains (optional)

ls-targets-demo        JOB=<job>                 - List Blackbox targets (demo)
add-target-demo        JOB=<job> TARGET=<url>    - Add target (demo)
rm-target-demo         JOB=<job> TARGET=<url>    - Remove target (demo)
```

## Links
Technical repo: https://github.com/hugomolinfresneda/homelab-stacks  
Monitoring entrypoint: https://github.com/hugomolinfresneda/homelab-stacks/blob/main/stacks/monitoring/README.md  
Makefile.demo: https://github.com/hugomolinfresneda/homelab-stacks/blob/main/stacks/monitoring/Makefile.demo  
Demo env template: https://github.com/hugomolinfresneda/homelab-stacks/blob/main/stacks/monitoring/.env.demo.example  
Runbooks: https://github.com/hugomolinfresneda/homelab-stacks/tree/main/stacks/monitoring/runbooks  
Backups: https://github.com/hugomolinfresneda/homelab-stacks/blob/main/ops/backups/README.md  
