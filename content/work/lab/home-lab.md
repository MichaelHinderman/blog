---
title: "Home Lab"
date: 2026-06-10
status: "Active"
featured: false
tags: ["networking", "security", "self-hosting"]
summary: "A small rack running segmented VLANs, a firewall, and the services behind my other projects. It's where Port Watch runs."
outcome: "Stable for six months. Next: central logging."
stack: ["Proxmox", "OPNsense", "Docker"]
---

## Layout

Three VLANs: trusted, IoT, and lab. The lab network is where anything experimental lives.
