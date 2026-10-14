# Grid — status

Living snapshot of what is **done**, **in progress**, and **planned**.  
The org profile stays short; update this file when priorities change.

Last updated: 2026-10-14

## Done

- Self-host control plane (Compose on VM + native optional)
- Desired-state GitOps (`grid-config`) + module bank (`grid-terraform`)
- Releases: plan / apply / destroy with live logs
- Remote Terraform state + archive mirror (S3 / GCS / Azure, …)
- AWS + GCP catalogs marked **supported** in `grid-cli`
- Network fabric / control desired-state examples
- Org profile README (centered) + localized variants; `grid-config` documented as example-only (create your own desired-state repository)
- Host monitoring plane (Prometheus + Alertmanager + Alloy); Alerts in console Settings
- Production boot gates for monitoring + remote state

## In progress

- Hardening AWS / GCP apply paths on a real control-plane VM (instance role / ADC)
- Packaging and public release polish (tags, install smoke)
- Demo video for the org README

## Planned

- Broader cloud release in the console (Azure and others behind flags today)
- Kubernetes operator (`grid-operator`)
- ML / assistant features (`grid-ml`)
- Additional docs site (Markdown in `grid-docs` remains canonical)

---

When something ships, move it to **Done**. When you start it, move it to **In progress**. Keep bullets short.
