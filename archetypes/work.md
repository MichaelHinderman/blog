---
title: "{{ replace .File.ContentBaseName "-" " " | title }}"
date: {{ .Date | time.Format "2006-01-02" }}
status: "Active"        # Active | Shipped | Paused (any word works; becomes a filter)
featured: false         # true = shows in "Selected work" on the home page
tags: []
summary: ""             # 2–3 plain-language sentences; this is what a recruiter reads
outcome: ""             # one line on where it stands
stack: []
links: []               # - name: "Source"
                        #   url: "https://..."
draft: true
---

Technical write-up goes here. It renders under "Details" on the project page.
