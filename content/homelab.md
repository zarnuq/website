---
title: "Homelab"
description: "A five-node Proxmox cluster where I build Kubernetes from the VMs up: OpenTofu, Ubuntu, kubeadm and GitOps."
---

My homelab is where I learn infrastructure by owning every layer of it: the hypervisors, the
network, the VMs, and the Kubernetes cluster on top, all built from code.

## Hardware

A **five-node Proxmox VE cluster** (`lab`) with **52 CPUs, 148 GiB of RAM and 3.9 TiB of
storage** between them.

![Proxmox datacenter summary: cluster "lab", 5 nodes online, 14 VMs, 52 CPUs, 148 GiB memory, 3.90 TiB storage](/images/homelab/proxmox-summary.png)

## What runs on it

- **pfSense** as a VM, routing the lab network and serving its DNS
- **Kubernetes:** six VMs — three control-plane nodes (`cp1`–`cp3`) and three workers (`w1`–`w3`), one of each on three different hosts so losing a host doesn't take down the cluster
- A **NixOS** services VM that hosts my self-hosted apps ([below](#self-hosted-services))
- A **NAS** VM that serves the media library over NFS
- A **Windows** VM, a **game** VM, and scratch VMs for testing
- **WireGuard** for getting back into the lab from outside

![Proxmox server view: hosts prox0–prox4 with the pfSense, Kubernetes, NAS, NixOS, Windows and game VMs](/images/homelab/proxmox-tree.png)

## Self-hosted services

Day-to-day services run on a single **NixOS** VM (8 vCPU, 24 GB RAM), configured declaratively:
each service is its own Nix module, and turning one on or off is a matter of commenting a line
and running `nixos-rebuild switch`.

- **nginx** reverse proxy in front of every app, with a wildcard Let's Encrypt certificate issued through Cloudflare DNS-01 challenges
- **Authelia** single sign-on: forward-auth in front of internal apps, and an **OIDC** provider for Forgejo and Grafana
- **Forgejo** for self-hosted Git
- **Vaultwarden** password manager and **Nextcloud** for files, backed by PostgreSQL and Redis
- **Jellyfin** media server, reading the library from the NAS over NFS, with **Seerr** for requests
- **Prometheus**, **node exporter** and **Grafana** for metrics, **Gatus** for uptime checks, and **Homepage** as the dashboard tying it all together
- Some apps run as **Podman** containers managed by NixOS, alongside native services
- **sops-nix** keeps every secret (API tokens, OIDC keys, app credentials) encrypted with age in the config, decrypted only on the host at activation

## The Kubernetes cluster

I'm building the cluster the long way, so I understand each layer instead of letting a
distribution hide it:

1. **OpenTofu** declares all six VMs in one file through the Proxmox API. Each node is one line in a map (VM ID, host, IP, cores, memory, disk), so adding or removing a node is a one-line change and `tofu apply`
2. **Ubuntu 24.04** cloud images, with **cloud-init** setting each VM's static IP and SSH key on first boot
3. **kubeadm** bootstraps Kubernetes on those VMs: three control-plane nodes for a highly available control plane, three workers for workloads
4. **GitOps** for everything after that: every workload and cluster service is a plain **Kubernetes manifest** in Git, and the cluster is reconciled from the repository, so Git is the single source of truth for what runs

## Stack

Proxmox VE · pfSense · WireGuard · NixOS · sops-nix · nginx · Let's Encrypt · Authelia (SSO / OIDC) ·
Podman · PostgreSQL · Prometheus · Grafana · NFS · OpenTofu · cloud-init · Ubuntu · kubeadm · Kubernetes · GitOps
