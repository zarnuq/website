---
title: "Homelab"
description: "A three-node Proxmox cluster where I build Kubernetes from the VMs up, with OpenTofu, Talos, Cilium and Flux."
---

My homelab is where I learn infrastructure by owning every layer of it: the hypervisors, the
network, the VMs, the Kubernetes cluster on top, and the tooling that builds it all from code.

## Hardware and network

- **Three Proxmox VE hosts** clustered together; Kubernetes nodes are spread across all three so losing one host doesn't take down the cluster
- **pfSense** routes the lab LAN and serves its DNS, including local overrides for internal hostnames
- **WireGuard** for getting back into the lab from outside

## The cluster

Six VMs — three control-plane nodes and three workers, one of each per Proxmox host — all
declared in a single **OpenTofu** file. Adding or removing a node is one line in a map followed by
`tofu apply`.

The first full build ran **Talos Linux**, an API-driven, immutable OS made only for Kubernetes:

- **OpenTofu** pulled a Talos image from Image Factory (with the QEMU guest agent baked in) onto each Proxmox host, created the VMs, generated the Talos machine configs, applied them, and bootstrapped the cluster — one command from empty hosts to a working kubeconfig
- A **floating virtual IP** shared by the control-plane nodes fronts the Kubernetes API, so the API stays reachable when a control-plane node goes down
- **Cilium** is the CNI and replaces kube-proxy entirely. It also hands out LoadBalancer IPs from a LAN pool and announces them over ARP (no MetalLB needed), and runs a shared ingress controller, with Hubble for network observability
- **Flux** does GitOps: the cluster reconciles itself from a Git repository, installing controllers first and the configuration that depends on their CRDs second
- **cert-manager** issues Let's Encrypt certificates through Cloudflare DNS-01 challenges, so internal services get real TLS without being exposed to the internet
- **ExternalDNS** keeps Cloudflare records in sync with the cluster's Ingresses and Services, and only touches records it owns
- **SOPS + age** encrypt secrets (like the Cloudflare API token) before they are committed, and Flux decrypts them in-cluster

## Rebuilding it the long way

Talos and Flux made the cluster easy to stand up, but they also hid a lot of how Kubernetes
actually comes together. So I'm rebuilding it from plain **Ubuntu 24.04** cloud images: OpenTofu
now only creates the VMs and cloud-init sets their networking and SSH keys. From there I prepare the
nodes and bootstrap Kubernetes by hand, then automate each step with **Ansible** only once I
understand it, and bring back Helm, Flux and the cluster services one layer at a time.

## Stack

Proxmox VE · OpenTofu · cloud-init · Talos Linux · Ubuntu · Kubernetes · Cilium · Hubble · Flux ·
Helm · Kustomize · cert-manager · ExternalDNS · Cloudflare · SOPS / age · pfSense · WireGuard · Ansible
