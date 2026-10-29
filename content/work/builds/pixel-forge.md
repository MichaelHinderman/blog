---
title: "Pixel Forge"
date: 2026-09-14
status: "Shipped"
featured: true
tags: ["games", "tooling", "graphics"]
summary: "A desktop pixel-art sprite editor with layers, onion skinning, and spritesheet export. I built it because existing tools made animation tedious."
outcome: "Used daily for Dungeon Run's art. First public release tagged."
stack: ["Rust", "egui"]
links:
  - name: "Source"
    url: "https://github.com/MichaelHinderman/pixel-forge"
---

## Design notes

The palette quantizer is custom. It reduces imported images to a fixed palette while keeping outlines crisp.

## What I'd do differently

Start with the file format. I changed it three times.
