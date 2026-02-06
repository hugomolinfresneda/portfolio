# Portfolio — Linux Operations & Observability

Production-inspired homelab portfolio: documented ops workflows, backup/restore runbooks, and Prometheus/Grafana observability patterns.

**Highlights**
- Operable-by-design stacks: consistent conventions, validation checks, and predictable workflows.
- Failure-aware docs: troubleshooting notes, runbooks, and recovery steps that assume things break.
- Actionable observability: metrics and logs wired into dashboards and alerting with runbooks.

**Primary links**
- Technical repo (code): [homelab-stacks][homelab-stacks].
- Case study (2–3 min): [case study][case-study].
- Demo script (5–7 min): [demo][demo].
- CV: [EN][cv-en] · [ES][cv-es].

---

## How to review in ~5 minutes
1. **Start here (30s):** skim this README and open [media/][media] (screenshots + architecture diagram).
2. **Read the case study (2–3 min):** [case-studies/homelab-stacks.md][case-study] (context, decisions, operations).
3. **Validate the technical repo (1 min):** open [homelab-stacks][homelab-stacks] and skim the main README + ops entrypoints.
4. **Interview-ready (optional):** follow [demos/homelab-stacks-demo.md][demo] for a short, copy/paste demo.

## Featured project: homelab-stacks
`homelab-stacks` is my main technical project: a collection of operable Docker Compose stacks built with day-2 operations in mind.

**What it demonstrates**
- Repeatable ops workflows (make-first) with clear runtime boundaries and templates.
- Reliability basics: healthchecks, safe procedures, and backup/restore guidance.
- Observability patterns: metrics + logs wired into dashboards, alerting and runbooks.

**Where to look**
- Entry points: [README][hs-readme] + core docs ([project contract][hs-contract] and [runtime overrides][hs-runtime-overrides]).
- Ops workflow: [Makefile][hs-makefile] (validation, stack lifecycle, day-2 operations).
- Monitoring: [monitoring README][hs-monitoring-readme] + [runbooks][hs-runbooks].
- Backup/restore: [documentation][hs-backups].

## Evidence pack
- **Case study (2–3 min):** [homelab-stacks case study][case-study] — context, decisions, tradeoffs, operations.
- **Demo script (5–7 min):** [homelab-stacks demo][demo] — copy/paste walkthrough for interviews.
- **Screenshots & diagram:** [media/][media] — dashboards, alert example, architecture overview.

## Skills (keywords)
Linux, systemd, Bash, Git, Docker, Docker Compose, DNS/TLS, Prometheus, Alertmanager, Grafana, Loki/Promtail, runbooks, backup/restore, CI checks.

## About
Junior-to-junior-high observability engineer focused on platform/toolchain and infra monitoring (RHCSA-level Linux fundamentals).

**Background**
- 24x7 multi-client monitoring: runbook-driven triage, recurring ops checks (backups, job queue health, SLAs), ITSM escalation (Helix/Jira), on-call for high severity.
- Observability service coordination for Banco Santander: led 8–12 operators (24x7), ~3k–5k alerts/day, typically 10–20 escalations/day.

**Focus**
- Signal over noise: actionable alerts, clear runbooks, structured escalation.
- Operability: runtime contracts, makefile-first workflows, backup/restore, Alertmanager + Loki/Promtail.
- Continuous improvement: post-incident reviews that update docs, alerts, and procedures.

**Now**  
Madrid-based. Hybrid/remote. No rotating shifts; paid on-call only. Prefer product environments.

## Contact
- **LinkedIn**: [hugomolinfresneda][linkedin]
- **Email:** hugomolinfresneda@gmail.com

---

*Personal lab / portfolio. Patterns are production-inspired; no support implied.*


[homelab-stacks]: https://github.com/hugomolinfresneda/homelab-stacks
[case-study]: case-studies/homelab-stacks.md
[demo]: demos/homelab-stacks-demo.md
[cv-en]: docs/cv-hugo-molin-en.pdf
[cv-es]: docs/cv-hugo-molin-es.pdf
[media]: media/
[hs-readme]: https://github.com/hugomolinfresneda/homelab-stacks#readme
[hs-contract]: https://github.com/hugomolinfresneda/homelab-stacks/blob/main/docs/contract.md
[hs-runtime-overrides]: https://github.com/hugomolinfresneda/homelab-stacks/blob/main/docs/runtime-overrides.md
[hs-makefile]: https://github.com/hugomolinfresneda/homelab-stacks/blob/main/Makefile
[hs-monitoring-readme]: https://github.com/hugomolinfresneda/homelab-stacks/blob/main/stacks/monitoring/README.md
[hs-runbooks]: https://github.com/hugomolinfresneda/homelab-stacks/tree/main/stacks/monitoring/runbooks
[hs-backups]: https://github.com/hugomolinfresneda/homelab-stacks/blob/main/ops/backups/README.md
[linkedin]: https://www.linkedin.com/in/hugomolinfresneda/
