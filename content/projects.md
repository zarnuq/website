---
title: "Projects"
description: "reach — a tiling Wayland window manager in Zig; lazygentoo — an Ansible Gentoo installer with LUKS, Secure Boot and TPM2; and more."
---

Everything below is public on [github.com/zarnuq](https://github.com/zarnuq).

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
