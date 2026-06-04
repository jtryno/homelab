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
| Ubuntu Server 24.04 | Primary VM, Ansible control node |
| Ansible | Configuration management and automation |
| Ansible Vault | Encrypted secrets management |
| Docker | Containerized services |
| ROCm 7.2.3 | AMD GPU compute stack |
| Ollama 0.30.4 | Local LLM inference server |

## Virtual Machines
| Name | IP | OS | Role |
|------|----|----|------|
| ubuntu-server | 192.168.1.x | Ubuntu Server 24.04 | Ansible control node, Docker host |
| homelab-02 | 192.168.1.x | Ubuntu Server 24.04 | General purpose |
| ollama-gpu | 192.168.1.x | Ubuntu Server 24.04 | Ollama GPU inference (RX 6600 XT) |

### Installed Models
| Model | Size | Use |
|-------|------|-----|
| llama3.2:3b | 2.0 GB | General purpose, fast |
| llama3.1:8b | 4.9 GB | General purpose, higher quality |
| qwen2.5-coder:14b | ~9 GB | Coding assistant |

## Repository Structure
```
homelab/
├── ansible/          # Playbooks, inventory, and variables
├── docker/           # Docker Compose files for services
└── proxmox/          # Notes and configuration references
```

## Goals
- Automate all server configuration with Ansible
- Deploy and manage services via Docker Compose
- Expand inventory with additional Proxmox VMs
- Document everything as code
- Learn!
