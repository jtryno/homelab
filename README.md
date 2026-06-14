# Homelab

Personal homelab built on an old PC running Proxmox VE. This repo documents the infrastructure, automation, and services I've built and manage.

## Hardware
- **CPU:** AMD Ryzen 7 5700X
- **RAM:** 64GB
- **Storage:** 500GB NVMe
- **Hypervisor:** Proxmox VE

## Stack
| Tool | Purpose |
|------|---------|
| Proxmox VE | Type-1 hypervisor, VM management |
| Ubuntu Server 24.04 | Base OS for all VMs |
| Ansible | Configuration management and automation |
| Ansible Vault | Encrypted secrets management |
| Semaphore UI | Web interface for running Ansible playbooks |
| Docker | Containerized services |
| Prometheus | Metrics collection and storage |
| Grafana | Metrics visualization and dashboards |
| Node Exporter | Host-level metrics exporter for Prometheus |
| GitHub Actions | CI/CD pipeline for automated linting |

## Virtual Machines
| Name | IP | OS | Role |
|------|----|----|------|
| ubuntu-server | 192.168.1.x | Ubuntu Server 24.04 | Ansible control node, Docker host |
| homelab-02 | 192.168.1.x | Ubuntu Server 24.04 | General purpose |
| monitoring-01 | 192.168.1.x | Ubuntu Server 24.04 | Prometheus, Node Exporter, Grafana |

## Repository Structure
```
homelab/
├── ansible/
│   ├── roles/
│   │   ├── common/         # Base packages, timezone, apt updates
│   │   ├── ufw/            # Firewall rules for all hosts
│   │   ├── node_exporter/  # Prometheus Node Exporter
│   │   ├── docker/         # Docker Engine and Compose
│   │   ├── monitoring_stack/ # Prometheus and Grafana via Docker Compose
│   │   └── semaphore/        # Semaphore UI and Postgres via Docker Compose
│   ├── playbooks/          # Scoped playbooks and site.yml orchestrator
│   ├── inventory/          # Hosts and group_vars
│   ├── collections/        # Ansible Galaxy requirements
│   └── ansible.cfg
├── semaphore/              # Docker Compose for Semaphore UI
└── proxmox/                # Notes and configuration references
```

## Notes

### Semaphore configuration
The `semaphore` role deploys the Semaphore container and its dependencies but you have to manually configure the following in the Semaphore UI after deployment:

- **Key Store**: SSH key (`~/.ssh/ansible_key`) and vault password
- **Inventory**: Static inventory using the `hosts.yml` structure
- **Variable Group**: `timezone`, `grafana_admin_password`, `postgres_password`, `semaphore_admin_password` as extra variables; `ANSIBLE_ROLES_PATH=ansible/roles` as environment variable
- **Repository**: GitHub repo URL and branch
- **Task templates**: One per playbook under `ansible/playbooks/`, with vault password attached and Galaxy install skipped

## Goals
- Automate all server configuration with Ansible
- Deploy and manage services via Docker Compose
- ~~Build a full monitoring stack with Prometheus and Grafana~~ (completed)
- ~~Deploy a web UI for Ansible playbook management~~ (completed)
- ~~Set up a full CI/CD pipeline with automated linting~~ (completed)
- ~~Refactor playbooks into Ansible roles~~ (completed)
- Expand inventory with additional Proxmox VMs
- Document everything as code
- Learn!!
