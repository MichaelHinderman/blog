---
title: "Resume"
description: "A long-form, technology-focused account of what I've built and run over ten years in security operations and automation."
ShowToc: true
TocOpen: false
---


## Summary

I have spent ten years in security operations, moving from SOC analyst to network forensics lead to security automation engineer to engineering manager. The through-line is automation: taking repetitive investigation and response work and turning it into reliable, reusable systems.

Most of that work has been on SOAR and SIEM platforms, chiefly Cortex XSOAR and XSIAM, with earlier years on Splunk and IBM QRadar. I write Python, build REST integrations against whatever stack a customer runs, and spend a lot of time teaching other engineers how to design automations that hold up in production. More recently I have built internal tooling on Google Cloud, BigQuery, Apps Script, and Gemini to give managers near-real-time visibility across a large customer base.

I currently manage a fourteen-engineer Customer Success Engineering team at Palo Alto Networks that deploys Cortex detection and response workflows into enterprise environments.

## Technical skills

**Languages and automation:** Python, Bash, JavaScript, Google Apps Script, REST API integration development, AI-assisted workflow automation.

**SOAR and SIEM:** Cortex XSOAR, Cortex XSIAM, Cortex AgentiX, Splunk, IBM QRadar. Playbook and integration development, detection content, data-source onboarding, classification and mapping, pre-processing, Docker and Podman engine management.

**Endpoint and analysis:** Cortex XDR, CylancePROTECT and OPTICS, FireEye AX, Wireshark and PCAP forensics, Tanium, Wazuh.

**Data and AI tooling:** Google BigQuery, Gemini, Apps Script, Claude Code, Gemini CLI, Codex, Ollama.

**Infrastructure:** Proxmox, OPNsense, VLAN segmentation, Active Directory, DNS and DHCP, Ubiquiti UniFi, nginx reverse proxies, DigitalOcean and AWS, NAS and cold-storage backup, AlienVault USM, Vectra.

**Response domains:** phishing response, threat hunting, identity and MFA response, IOC correlation and enrichment, DLP, cloud remediation, ITSM orchestration with ServiceNow and Jira.

## Experience

### Palo Alto Networks: Engineering Manager, Cortex Deployment

*Customer Success Engineering, March 2025 to present, remote*

I lead a fourteen-engineer team that deploys XSOAR, XSIAM and Cortex Cloud detection and response workflows into enterprise environments. The team covers roughly three hundred customers across eight Cortex products. I restructured it from a generalist model, where everyone covered every product, into specialized sub-roles: Technical Account Manager, Delivery Engineer, and Content and Scale. Customer engagement now routes through a defined process, which cut context switching and closed depth-of-expertise gaps. I also ran an XSIAM cross-training program that got half the team certified as XSIAM Analysts.

I still take on hands-on automation, playbook, and integration requests across AgentiX, XSIAM, and XDR. They share the same automation foundation as XSOAR, and most of those requests come down to teaching the product rather than fixing it. Getting a customer self-sufficient is the job, and that was true when I was an engineer too.

#### Portfolio-intelligence portal

With three hundred customers and limited account-management coverage, managers could not get an accurate picture of a customer's technical health without chasing several teams for hours. Engineers write notes from their own perspective, and asking technical people to answer business questions on demand does not scale. I built a portal to answer those questions directly from the data.

The application runs in Google Apps Script and has two halves. A scheduled pipeline pulls each customer's data from BigQuery, Asana, Google Sheets, Salesforce, Gainsight, and Tableau. It computes deterministic metrics and writes them back to BigQuery. It then runs three to four targeted Gemini queries per customer against the same data and stores those results too, so the questions I care about are already answered when I open the portal instead of being asked repeatedly by hand.

One of those queries is a renewal-risk assessment. It weighs time to renewal, open support cases, and the tone of the customer's case comments, including whether that tone is normal for them or has shifted over time. I compare that AI-derived sentiment with the human-entered sentiment from the account team. Where they diverge, there is usually a problem that has not been reported yet. This has caught frustration early many times and also surfaces patterns across customers, like a single event affecting sentiment across many customers.

The front end lets me filter customers, read bottom-line-up-front summaries, pick a time window and one or many customers, and ask ad hoc questions of Gemini scoped to that data. That is how I prepare weekly executive reviews. The project was adopted by the internal tools team, rebuilt as a supported product, and is now used by the customer success executive team and other post-sales teams.

#### Audit of 1,200 unstructured activity records

During a two-month period when our normal tracking tooling was unavailable, engineers recorded customer meetings in free-text notes. At the end of the half, managers had two weeks to extract measurable high-impact outcomes from about 1,200 of those records to report against team goals. I defined what counted as a high-impact outcome and built the pipeline to find them.

Throwing the notes at Gemini did not work. An engineer working the same project across several sessions produced the same outcome many times over, and hallucinated outcomes were common. The pipeline instead grouped records by engineer and customer, identified the distinct activities inside each group, deduplicated activities across sessions, and only then classified them. That cut the noise from two or three hundred candidate outcomes per engineer to a defensible ten to twenty, which matched what people actually did. It saved forty-plus manual hours and, more importantly, produced numbers leadership could trust. I followed it with documentation standards across 1,500-plus activity records mapped to customer journey milestones.

#### Deployment engagement framework

A customer's first use cases were traditionally heavy: phishing or malware response, taking three to six months to build. Customers sat with a platform that produced no value in the meantime. I led a three-engineer taskforce to find content we could stand up in a day.

We settled on a bundle that targets the incident type every new customer has the most of: generic, uncategorized incidents. The content extracts indicators from those incidents, enriches and analyzes them automatically, and writes findings back to the incident so nobody has to triage hundreds of raw alerts by hand. A scheduled job then sweeps those incidents, pulls out the important findings, and emails a periodic report to the administrator. The bundle also adds platform-level operational reporting, such as MTTR, MTTD, ingested versus closed incident counts, and data volume, plus basic connectors from XSOAR and XSIAM to external AI services for on-demand analysis.

Each piece can be switched off per customer. We install everything and disable what they do not want. Because it runs on anything routed to the default incident type, it works while real integrations are still being onboarded. The team doubled its production go-live target for the half.

#### Playbook standards

I standardized production playbook frameworks for phishing response, threat hunting, cloud remediation, DLP, and network and firewall use cases. The two principles behind them come from years of fixing other people's automations.

First, normalization and intent. Every piece of data has a defined place, name, and meaning, and a clear statement of what it is for. An email address stored as just "email" can be a victim, a sender, or an active indicator, and a downstream playbook that searches it against a public service may tip off an attacker. Playbooks written for one problem define their own schema, which works until a second author or a second runbook shows up.

Second, gate every action. A query that happens to return one row today will someday return fifteen hundred, and the ticket-creation step after it will open fifteen hundred Jira tickets. Playbooks are applications, not scripts. Checking inputs and bounding outputs before an action costs minutes and saves weeks of troubleshooting. Teaching teams these two ideas does more for their competence than fixing any single playbook, and it is what lets them treat content as interchangeable Lego pieces rather than bespoke builds.

### Palo Alto Networks: Principal Engineer

*Previously Senior Technical Lead and Customer Success Engineer, March 2020 to March 2025, remote*

I deployed XSOAR to production in twenty-nine enterprise environments, with playbooks for endpoint response, identity and MFA lockout, IOC correlation, and ITSM orchestration. I was the primary technical escalation point for the fourteen-engineer team and the broader Cortex organization while carrying the team's highest customer volume. I acted as interim team manager for two months, running one-on-ones, workload balancing, escalations, and executive reporting. I onboarded and mentored about half of the team's new hires through shadowing and training programs.

#### How I approach the platform

Strip the security vocabulary off XSOAR and it is a data aggregation, filtering, and automation platform. When I joined, I learned its internals by building a Pokémon game in it: an integration against the public PokéAPI pulled the data, incidents became encounters, the incident layout rendered the battle, player state lived in lists and integration context, and scripts handled combat, leveling, and evolution. It sounds like a joke, but it proved the point. The platform can be a CRM, a help desk, or a DevOps tracker.

That shapes how I build integrations. I follow the path of the data, not its meaning. An IP address, a username, and a ticket ID are all strings. A list is a list. Once you see the shape of the data moving through an API, writing or debugging an integration against any EDR, identity provider, ticketing system, or threat-intel feed becomes the same exercise.

#### Custom integrations

I developed custom XSOAR integrations in Python against customer REST APIs across EDR, identity, ticketing, and threat intelligence platforms, closing coverage gaps where no packaged content existed.

#### Unblocking a stalled bank deployment

A large bank's XSOAR deployment had been stalled for about a year. The root cause was not one bug. The platform ran on Docker, which the bank was phasing out by policy, so the engine had to move to Podman. Nobody on the customer's DevOps team knew Podman or Linux internals well enough to do it, the systems were air-gapped, and every change had to fit inside scheduled change windows with audit sign-off.

I worked as the subject matter expert on XSOAR, Linux, and containers at once. While we waited six months for the first change window, I rebuilt their content: temporary playbooks rerouted live investigation workflows around integrations that could not reach internal services, and orchestrated the deployment plans for XSOAR engines inside their network to give the platform access it previously lacked, using those engines as the test bed for defining the Podman installation process.

The first change window exposed problems we had not anticipated: cgroupsv2 and  systemd configuration, permission restrictions, and no access to current package versions on air-gapped hosts. We did not finish, and planned across several more windows. In the final window we migrated step by step over two weeks of ten-hour calls, reviewing each command, with a rollback ready at every stage. The platform came out stable, the content was updated to the proper integrations, and the team passed the audits which had flagged their servers. I was promoted to Engineering Manager shortly after.

#### XSOAR 6 to 8 migration tracking

Customer Success needed a way to track the full XSOAR customer base through the XSOAR 6 to 8 SaaS migration, especially on-premises customers outside telemetry. I built the system the organization adopted: Apps Script behind Google Sheets, pulling from internal data sources and direct customer communication. The code enforced data integrity against backup versions of the sheet so an accidental revert never lost state, and it throttled reminders so customers who had already upgraded were not re-engaged. It also tracked each customer's migration status, which let us staff XSOAR 6 and 8 customers separately and point new engineers at 8 only. I co-led a three-engineer taskforce that re-engaged most of a large set of dormant environments during this period.

#### Training content

I authored a video series on Palo Alto's LiveCommunity, available to registered users. The core series covers the XSOAR incident lifecycle as a data flow: origination, ingestion through an integration, classification, mapping, pre-processing, incident creation, and post-incident states. The goal was to create a mental map of how XSOAR operated  so an engineer can locate where a content bug actually lives instead of patching it in a playbook. Other videos cover how XSOAR uses Docker, specifically watermarks: why they exist, how to monitor them, and how to design content that does not overload the engine, which is still a common cause of slow or crashed instances. A third set covers classification and mapping, a topic I explained so often that a video was a better use of everyone's hour.

#### Hackathons

I led a cross-functional hackathon of sixteen to twenty engineers and architects on the theme of "content that teaches rather than does". The winning approach was content with deliberate holes. Instead of delivering a finished playbook, the engineer delivers a working skeleton with marked gaps, explains how it works, and asks the customer to fill the gaps before the next session, with links to training. It shifts the weekly call from "let me fix this" to "what did you try, and why." Customers who engage become self-sufficient faster and renew more reliably. Those who will not engage are a renewal risk we can now see early.

### BlackBerry Cylance: CFC Analyst and Engineer

*March 2019 to March 2020, Plano, Texas*

I worked L1 and L2 security operations in a small team of two or three on shift, before the organization had a SOAR platform. Alerts arrived through Splunk and ServiceNow, and investigations meant hitting the same systems repeatedly by hand.

#### Phishing analysis tool

Phishing investigations took fifteen to forty-five minutes each, mostly data gathering. I wrote a local Python application that accepted an exported email file, parsed out every indicator, and tagged each by role, such as original sender or suspected payload. I could then choose which indicators to search against which services. That selectivity mattered: searching an active indicator against a public service can tip off an attacker, and this is where I learned to treat IOC lookups as a deliberate choice. The tool queried our internal services over their APIs, including Splunk and Tanium, flagged indicators matching known campaigns or training exercises, and generated the report. Analysis time dropped to five to fifteen minutes and a shift's queue of ten to fifteen emails cleared in under an hour. The case it made for automation led directly to the team adopting Demisto.

#### Demisto playbooks and standards

I designed a playbook tier system that went into production, built end-to-end playbooks automating analysis of Splunk-sourced alerts, and wrote the team's SOAR development standards covering automations, playbooks, jobs, incident templates, and integrations. In hindsight the tier system was an early form of the Lego approach I still teach: inputs with a defined structure, validation before any command runs, and explicit conditions for each action. Demisto at the time had little built-in error handling, so the standards were how two authors could write content that connected without clashing.

#### Investigation and forensics

I triaged and remediated alerts across platforms and ran on-demand threat hunts with written reports for leadership. For FireEye AX detonations I went past the portal's summary into the raw PCAP in Wireshark, drawing on my GNFA training. I wrote each investigation as a timestamped story across proxy, firewall, endpoint, and network sources with my own risk assessment, so the incident response team could read one to three paragraphs and know what happened before they spent time of their own.

### Wipro Limited (MSSP): SOC L3, Network Forensics Lead

*June 2017 to March 2019, Dallas, Texas and client sites*

I earned the GIAC Network Forensic Analyst certification during this time and became the network forensics lead for a sixty-person fusion center, with my own tooling and lab.

#### Breach forensics

WannaCry was active. I analyzed captures from healthcare and manufacturing clients, among others, to establish what happened and when, extract indicators, and cross-check them against public reporting. The kill-switch domain lookup was the fastest compromise signal, so I turned the analysis into a script that took a PCAP and returned a focused WannaCry assessment. We ran it across incoming captures from many clients and returned quick summary reports. I also delivered removable and disk drive analysis for healthcare clients and multi-cloud platform analysis for manufacturing clients.

#### QRadar

I monitored and tuned QRadar offenses and developed detection use cases and analysis procedures for L1 and L2 analysts, spanning generic incident response, identity and access, and endpoint detection. This is where I learned alert tuning the hard way, through trial and error.

#### Bank audit remediation

I spent three months on site in Washington, D.C. with a global bank that had failed an internal audit. Working directly with the IT director, I managed a list of fifty to sixty findings and fixed them. The network was flat, so I worked with the bank's infrastructure teams in the Middle East to redesign and resegment it with VLANs, including physical work in the server room and at the off-site disaster recovery office: rerouting cabling, installing new hardware, and decommissioning old. Endpoint protection and monitoring agents were badly out of date and were brought current. ACL monitoring and process documentation rounded out the list. The bank passed at the end of the engagement.

#### SOC design for a streaming media provider

I authored two documents for a California media company building its own SOC. The operations overview, about fifteen pages, told executives what the SOC would do, how, and with which tools. The analyst workflow document, about twenty-five pages, is a training manual on how to think like an L1 analyst: how to reason about a problem rather than which button to press, with flowcharts for each workflow. I reviewed requirements and status monthly with their security director and CISO. I reused the analyst document for years to train new analyst cohorts at Wipro.

#### Training and the SOC lab

I built and delivered analyst training in access control, networking, Python, Linux, and forensics. The SOC lab began as a side project with seven or eight of us on a secondhand server rack, running QRadar, Vectra, Demisto, and simulated malware and forensic networks. Leadership saw the value, formalized it on properly provisioned hardware on the Wipro network, and it became a secure environment for customer analysis and malware execution that was offered as a service.

### Cyber Defense Labs: SOC Intern

*May 2016 to June 2017, Richardson, Texas*

I monitored AlienVault USM alerts and wrote incident reports, learned virtual firewall deployment and assisted a deployment in a Dallas data center, and wrote a red team operations knowledge document to check my understanding against the team's. I sat in on red team engagements to learn what operators touch, what they avoid, and how authorization letters work in practice. I was given ownership of a social engineering operation: cold-calling 150 employees of an authorized client to get them to sign in to a cloned login page. The provided script did not work, so I rewrote it. Once I had someone on the line, I got a successful login about eight times out of ten by adjusting accent and word choice, calming concerns, and letting the target feel in control of the conversation. I also helped set up a Raspberry Pi Minecraft server network for a children's security workshop.

## Home lab

I run an enterprise-style network at home on Proxmox with OPNsense as the primary firewall. Traffic is split into VLANs: security tools, DNS and DHCP, logging, a Windows host managing Ubiquiti access points, a wireless-client segment, a public-services segment, and an administrative segment. A single machine on the admin VLAN is the only one allowed to reach the firewall and Proxmox management interfaces, and firewall rules block most inter-VLAN traffic. Every endpoint runs a Wazuh agent reporting to a Wazuh server on the security VLAN.

The public-services VLAN hosts an internal website and game servers behind an nginx reverse proxy. A second nginx instance on DigitalOcean fronts it, so public DNS points at a stable cloud IP rather than my home address, and Cloudflare provides monitoring that would be harder to run locally. A locally hosted VPN and a NAS with a cold-storage backup strategy round it out, plus a dedicated pentest lab segment. A local XSOAR instance handles basic lab alerting and remains a sandbox for content development.

## Certifications

- Palo Alto Networks XSOAR Engineer, 2024, active
- PCSAE, Palo Alto Networks Certified Security Automation Engineer, 2021, inactive
- GIAC Network Forensic Analyst (GNFA), analyst number 1571, 2018, inactive

## Education

**University of North Texas, B.S. Information Technology, 2012 to 2017, Denton, Texas**

A group of us revived the dead cybersecurity club, and I served as its vice president for the engineering department. To recruit, I built a ten-stage capture-the-flag for the engineering department over two months. Each stage fed the next, fifty people entered, and one finished. Afterward I walked everyone through every stage, covering hashes, Telnet access, buffer overflows, WiFi exploitation, Linux, and Python, which brought in many new members. I competed in the Collegiate Cyber Defense Competition in 2016 and 2017. Six hours of defending unfamiliar systems under pressure, while keeping a mock leadership team informed, taught me more about running a network than any class.
