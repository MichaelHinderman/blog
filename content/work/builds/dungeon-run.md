---
title: "Dungeon Run"
date: 2026-07-02
status: "Active"
featured: true
tags: ["games", "godot"]
summary: "A roguelike with procedurally generated floors. I'm using it to learn Godot properly and to dogfood Pixel Forge."
outcome: "Playable prototype with five floor types."
stack: ["Godot", "GDScript"]
---

## Generation

Floors are built from a room graph first, then carved into tiles. Keeps layouts connected without post-processing.
