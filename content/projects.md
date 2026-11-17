---
title: "Projects"
description: "ferrite — an intercepting proxy in Rust; Doc Works — an Obsidian plugin with 1,500+ downloads; reach — a tiling Wayland window manager in Zig; lazygentoo — an Ansible Gentoo installer; and more."
---

Most of what follows is public on [github.com/zarnuq](https://github.com/zarnuq); private work is marked as such.

## ferrite

**Rust** · [github.com/zarnuq/ferrite](https://github.com/zarnuq/ferrite) · Oct 2026 – present

A Burp Suite-style intercepting proxy for web application penetration testing, written in Rust with
an egui interface.

- **Proxy:** HTTP/1.1, HTTP/2 and WebSockets, TLS MITM with a generated CA, intercept, match & replace, scope, upstream HTTP/SOCKS5
- **Manual tools:** Repeater, WebSocket Repeater, Intruder (all four attack types), Sequencer, Decoder, Comparer
- **Automated:** passive and active scanner, crawler, content discovery, race-condition tester, authorization comparison across identities, OpenAPI/Postman/GraphQL/WSDL import
- Python extension SDK, project files, HAR import/export; packaged as a live ebuild in my Gentoo overlay

## Doc Works & HTML Works

**TypeScript** · [Doc Works](https://github.com/zarnuq/DocWorks) · [HTML Works](https://github.com/zarnuq/HTMLWorks) · GPL-3.0 · Oct 2026 – present

A matching pair of plugins, both listed in the official Obsidian community plugin directory.
**Doc Works** opens and edits Word, PowerPoint and Excel files inside Obsidian and has passed
**1,500 downloads**. **HTML Works** previews `.html` files and edits their source in Obsidian's own
editor, with Vim motions and editor extensions.

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

## lazi

**Rust** · [github.com/zarnuq/lazi](https://github.com/zarnuq/lazi) · Sep 2026 – present

A terminal workspace whose main tab is a fast three-column file manager in the style of yazi and
ranger — vim keys, image previews over kitty's graphics protocol — plus a git tab that shows the
status of every repository under your project folders. Every key, previewer and opener comes from
config files. Packaged in my Gentoo overlay.

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
| [gendtree](https://github.com/zarnuq/gendtree) | Rust | Graphical dependency browser for Gentoo Portage — tree and column views, and *why is this installed* back to `@world`. Single binary |
| [musicmux](https://github.com/zarnuq/musicmux) | Python | Curses TUI that cleans up a music library: dedupes by decoded audio, quarantines broken files, re-tags from MusicBrainz + Deezer. Every change is reviewed and reversible |
| [canvasDL](https://github.com/zarnuq/canvasDL) | Python | Browse and bulk-download Canvas LMS courses from a TUI or through an MCP server, signing in via Microsoft SSO |
| [blue-scripts](https://github.com/zarnuq/blue-scripts) | Shell | Personal blue team scripts |
| [ncae-scripts](https://github.com/zarnuq/ncae-scripts) | Shell | Scripts for NCAE Cyber Games |
| [dotfiles](https://github.com/zarnuq/dotfiles) | — | Linux desktop configuration |
