---
title: "Projects"
description: "reach — a tiling Wayland window manager in Zig; lazygentoo — an Ansible Gentoo installer with LUKS, Secure Boot and TPM2; and more."
---

Most of what follows is public on [github.com/zarnuq](https://github.com/zarnuq); private work is marked as such.

## netdash

**Go** · private repository

A self-hosted homepage that doubles as a hand-authored, live network map. One
[KDL](https://kdl.dev) file describes every host and how they connect; a small Go server probes each
one and serves two views off the same status feed — a **dashboard** of service tiles with status
lights and uptime percentages, and a **map**, an auto-laid-out topology graph derived from how hosts
uplink into each other. Nodes turn red in both views the moment a check fails.

- **Topology is declared, not discovered.** Nesting in the config *is* the uplink, so there is no separate edge list to drift out of sync — declare a host once, reference it by id
- **Strict-parsed config:** unknown properties are an error and every id must resolve, so typos fail the load loudly rather than silently dropping a node
- **HTTP and TCP probes only** — deliberately no ICMP, which would need raw-socket privileges that complicate containers; a TCP connect answers "reachable?" without them
- **SQLite-backed history** with a windowed uptime API
- **Ships as a single static binary** — frontend embedded with `//go:embed` and a pure-Go SQLite driver, so no cgo, no sidecars, no runtime dependencies
- Cytoscape.js + dagre for topology layout; deploys into scratch/distroless

## reach

**Zig** · [github.com/zarnuq/reach](https://github.com/zarnuq/reach) · active since Jun 2026

A custom tiling Wayland window manager built on the [river](https://codeberg.org/river/river)
compositor's window-management protocol — roughly **5,900 lines of Zig**.

- Built-in status bar
- Window rules and multi-monitor support
- Live config reload
- Virtual desktops

## lazygentoo

**Ansible / Shell** · [github.com/zarnuq/lazygentoo](https://github.com/zarnuq/lazygentoo) · May – Jul 2026

A custom Gentoo Linux installer driven by three modular Ansible playbooks.

- Partitions disks with **LUKS** full-disk encryption
- Builds a custom kernel and deploys a prebuilt Catalyst stage4 image
- Automates **Secure Boot** key enrollment and kernel image signing
- **TPM2** auto-unlock of the encrypted root, bound to Secure Boot state (PCR 7)

Related: [gentoo-overlay](https://github.com/zarnuq/gentoo-overlay), a personal ebuild repository.

## Other work

| Project | Language | What it is |
|---|---|---|
| [zhimmer](https://github.com/zarnuq/zhimmer) | Shell (zsh) | A zsh plugin, ~2,600 lines, with benchmarks in the README. 0BSD |
| [pweq](https://github.com/zarnuq/pweq) | Python | PipeWire config generator from an EQ file — replaces EasyEffects and lsp-plugins. MIT |
| [gentoo-overlay](https://github.com/zarnuq/gentoo-overlay) | Shell | Personal Gentoo ebuild repository |
| [musicmux](https://github.com/zarnuq/musicmux) | Python | ~3,900-line Python application |
| [blue-scripts](https://github.com/zarnuq/blue-scripts) | Shell | Personal blue team scripts |
| [ncae-scripts](https://github.com/zarnuq/ncae-scripts) | Shell | Scripts for NCAE Cyber Games |
| [gendtree](https://github.com/zarnuq/gendtree) | Python | Small utility |
| [dotfiles](https://github.com/zarnuq/dotfiles) | — | Linux desktop configuration |
