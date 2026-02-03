# Hugo Molín — Monitorización y Observabilidad (Junior) | Linux (RHCSA)

**Ubicación:** Madrid, España · **Modalidad:** Híbrido/Remoto (área de Madrid)  
**Email:** hugomolinfresneda@gmail.com  
**LinkedIn:** https://linkedin.com/in/hugomolinfresneda/ · **GitHub:** https://github.com/hugomolinfresneda  
**Portfolio:** https://github.com/hugomolinfresneda/portfolio  
**Repo técnico:** https://github.com/hugomolinfresneda/homelab-stacks

---

## Resumen
Ingeniero junior de monitorización y observabilidad centrado en alertas accionables, runbooks y operaciones repetibles. Experiencia en entornos 24/7 de monitorización multi-cliente y en coordinación de un servicio de observabilidad para Banco Santander. Certificación RHCSA y experiencia práctica operando Prometheus/Grafana/Alertmanager y Loki/Promtail en entornos Docker/Compose.

## Competencias clave
**Observabilidad/monitorización:** Prometheus, Grafana, Alertmanager (enrutado), Loki, Promtail, Blackbox Exporter (sondas sintéticas), dashboards, ajuste de alertas (alert tuning), runbooks  
**Linux:** fundamentos a nivel RHCSA, systemd, fundamentos de redes, scripting en shell  
**Contenedores:** Docker, Docker Compose  
**Operación:** triaje de alertas e incidencias, flujos de escalado, coordinación con guardias, informes de SLA/métricas, acciones de seguimiento post-incidente, comunicación con proveedores  
**Herramientas:** Git, automatización basada en Makefile, ITSM (BMC Helix / Jira)

## Experiencia

### Coordinador del Servicio de Observabilidad (externalizado) — Banco Santander (Madrid) | 2025 (6 meses)
- Coordiné las operaciones del día a día de un servicio de observabilidad 24/7 (8–12 operadores); siendo el punto de contacto principal entre el cliente y el equipo de servicio.
- Mejoré la calidad de señal reduciendo escalados erróneos y ajustando procedimientos; reduje la incertidumbre del equipo con runbooks y documentaciones más claras.
- Representé al servicio en war rooms y post-mortems; impulsé acciones de seguimiento para actualizar runbooks y verificaciones operativas.
- Gestioné un incidente de proveedor que afectó a la monitorización sintética móvil (Sauce Labs): detecté una indisponibilidad imprevista, informé al cliente y a los equipos internos, y aseguré un relevo consciente entre turnos; posteriormente propuse automatizar con el proveedor el basculado a otro CPD ante incidentes similares.
- Operé con alto volumen (3k–5k alertas/día; normalmente 10–20 escalados al cliente/día), priorizando escalado rápido, preciso y claro.

### Operador de Monitorización Multi-cliente — Inetum (Madrid) | 2023–2025
- Realicé triaje de alertas en un entorno 24/7 multi-cliente siguiendo runbooks; resolví incidencias sencillas y escalé vía ITSM (BMC Helix / Jira) con contexto claro y siguientes acciones.
- Ejecuté verificaciones operativas recurrentes (validación de backups, salud de jobs/colas incluyendo Control-M) y generé informes de SLA/métricas para clientes.
- Di soporte al despliegue y mantenimiento de la monitorización (agentes Checkmk, Nagios) y gestioné casos con proveedores por email/teléfono en inglés.
- Coordiné incidencias de conectividad con ISPs para restaurar el servicio en sedes del cliente.

### Experiencia adicional
- Partner Success Representative — Payflow | 2022
- Soporte negocios (proyecto piloto) — Yoigo | 2021

## Proyectos

### homelab-stacks (GitHub) — Stacks Docker operables con monitorización y backups
- Diseñé un repo reproducible y orientado a operación: contrato de runtime explícito, entrypoints predecibles y evidencia de operabilidad en producción (dashboards, alertas, runbooks).
- Implementé un stack de monitorización (Prometheus/Grafana/Loki/Alertmanager) con dashboards desarrollados a medida, runbooks y enrutado de Alertmanager a Telegram.
- Construí un modo demo con una única plantilla `.env` y entrypoints en Makefile; workflow para añadir y eliminar targets de Blackbox con señal visible de recarga de Prometheus.
- Añadí herramientas de backup/restore con Restic y métricas en Grafana para comprobar estado y antigüedad de backups, fallos, duración y tendencias.

## Educación y certificaciones
- **Red Hat Certified System Administrator (RHCSA), EX200** — 2025
- **FPGS ASIR — Administración de Sistemas Informáticos en Red** — 2021–2023

## Idiomas
Español (nativo) · Inglés (C1)
