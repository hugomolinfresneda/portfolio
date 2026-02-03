# Hugo Molín — Monitoring & Observability (Junior) | Linux (RHCSA)

**Location:** Madrid, Spain · **Work mode:** Hybrid/Remote (Madrid area)  
**Email:** hugomolinfresneda@gmail.com  
**LinkedIn:** https://linkedin.com/in/hugomolinfresneda/ · **GitHub:** https://github.com/hugomolinfresneda  
**Portfolio:** https://github.com/hugomolinfresneda/portfolio  
**Tech repo:** https://github.com/hugomolinfresneda/homelab-stacks

---

## Summary
Junior Monitoring & Observability engineer focused on actionable alerting, runbooks, and repeatable operations. Background in 24/7 multi-client monitoring and observability service coordination for Banco Santander. RHCSA-certified with hands-on experience operating Prometheus/Grafana/Alertmanager and Loki/Promtail in Docker/Compose environments.

## Core skills
**Observability:** Prometheus, Grafana, Alertmanager (routing), Loki, Promtail, Blackbox Exporter (synthetic probes), dashboards, alert tuning, runbooks  
**Linux:** RHCSA-level fundamentals, systemd, networking fundamentals, shell scripting  
**Containers:** Docker, Docker Compose  
**Operations:** incident triage, escalation workflows, on-call coordination, SLA/metrics reporting, post-incident follow-ups, vendor coordination  
**Tooling:** Git, Makefile-driven ops automation, ITSM (BMC Helix / Jira)

## Experience

### Observability Service Coordinator (outsourced) — Banco Santander (Madrid) | 2025 (6 months)
- Coordinated day-to-day operations for a 24/7 observability service (8–12 operators); primary interface between the client and the outsourced team.
- Improved signal quality by reducing mis-escalations and tightening procedures; reduced operator uncertainty with clearer runbooks and documentation.
- Represented the service in war rooms and post-mortems; drove follow-ups to update runbooks and operational checks.
- Handled a vendor incident impacting mobile synthetic monitoring (Sauce Labs): detected unplanned downtime, informed the client and internal teams, and ensured clean handoff across shifts; later proposed automating failover requests with the vendor for similar incidents.
- Managed high-volume operations (3k–5k alerts/day; typically 10–20 client escalations/day), prioritizing fast, accurate escalation and clear incident comms over noise.

### Multi-client Monitoring Operator — Inetum (Madrid) | 2023–2025
- Performed 24/7 alert triage in a multi-client environment using runbooks; resolved straightforward issues and escalated via ITSM (BMC Helix / Jira) with clear context and next actions.
- Ran recurring operational checks (backup verification, job/queue health including Control-M) and produced SLA/metrics reporting for clients.
- Supported monitoring rollout and maintenance (Checkmk, Nagios agents) and handled vendor cases over email/phone in English.
- Coordinated connectivity incidents with ISPs to restore service at customer sites.

### Additional experience
Payflow — Partner Success Representative (2022) · Yoigo — Business Support, pilot project (2021)

## Projects

### homelab-stacks (GitHub) — Operable Docker stacks with monitoring + backups
- Designed a reproducible ops-focused repo: explicit runtime contract, predictable entrypoints, and evidence for day-2 operations (dashboards, alerts, runbooks).
- Implemented a monitoring stack (Prometheus/Grafana/Loki/Alertmanager) with curated dashboards, runbooks, and Alertmanager routing to Telegram.
- Built a demo mode with a single `.env` template + Makefile entrypoints; Blackbox target add/remove workflow with a visible Prometheus reload signal.
- Added backup/restore tooling with Restic and Grafana metrics for backup freshness, failures, duration, and trends.

## Education & certifications
- **Red Hat Certified System Administrator (RHCSA), EX200** — 2025
- **Higher National Diploma (HND) — Administration of Networked Computer Systems (ASIR)** — 2021–2023

## Languages
Spanish (native) · English (C1)
