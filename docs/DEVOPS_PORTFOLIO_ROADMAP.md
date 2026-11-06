# DevOps Portfolio Roadmap

This roadmap tracks the Telegram-bot delivery project: taking one application
through a modern delivery pipeline, on-premises and in the cloud.

## Delivery stages

- [x] **Phase 0** — GitHub & dev workstation setup
- [ ] **Phase 1** — Linux automation with Bash
- [ ] **Phase 2** — Containerization with Docker
- [ ] **Phase 3** — CI/CD with GitHub Actions
- [ ] **Phase 4** — Infrastructure as Code (Ansible + Terraform on vSphere)
- [ ] **Phase 5** — Kubernetes deployment with Helm & GitOps (ArgoCD)
- [ ] **Phase 6** — Monitoring & alerting (Prometheus, Grafana, Loki)
- [ ] **Phase 7** — Cloud deployment on AWS with Terraform

These checkboxes apply to this application's delivery pipeline. Work completed
in another project does not automatically complete a stage here. For example,
[OVA Exporter GUI](https://github.com/abdomitov/ova-exporter-gui) already has
automated tests and GitHub Actions; the bot pipeline remains tracked separately.

## Related work

- [Homelab infrastructure](../README.md) — cluster configuration and deployment notes.
- [vCenter monitoring](https://github.com/abdomitov/vcenter-monitoring) — its monitoring and Telegram reporting roadmap stays in that repository.
