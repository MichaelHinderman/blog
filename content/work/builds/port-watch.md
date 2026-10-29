---
title: "Port Watch"
date: 2026-08-20
status: "Paused"
featured: false
tags: ["security", "networking"]
summary: "A scheduled network monitor that diffs open ports against a baseline and alerts on anything new."
outcome: "Runs on my lab network. Alerting works; the web dashboard is unfinished."
stack: ["Python", "nmap", "SQLite"]
---

## How it works

A cron job scans a host list, stores results in SQLite, and compares against the last accepted baseline. Differences go to a webhook.
