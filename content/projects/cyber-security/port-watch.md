---
title: "Port Watch"
date: 2026-08-20
summary: "A lightweight network monitor that alerts on unexpected open ports."
tags: ["security", "networking"]
---

## What it is

Port Watch runs on a schedule, scans a host list, and diffs the results against a baseline. New open ports trigger an alert.

## Stack

- Python, nmap
- SQLite for baselines
