# Splunk SOC Lab — Log Analysis, Detection Engineering & Alerting

Author: DeCyberGuardian  

Purpose: Build a SOC-style environment ingesting Windows (Sysmon + Event Logs) and Linux logs into Splunk. Create detections, dashboards and playbooks mapped to MITRE ATT&CK.

## Architecture
- Ubuntu VM: Splunk Enterprise (Indexer + Search Head)
- Windows 11 VM: Endpoint; Sysmon + Splunk Universal Forwarder (UF)
- Kali VM: Attacker & testing host for generating telemetry

Data flow:
Windows Events & Sysmon -> Splunk UF -> Splunk Indexer (index=sysmon, index=winevent)
Linux logs -> Splunk UF or local forwarder -> Splunk Indexer (index=linux)

## Goals / Deliverables
1. Reproducible lab instructions (Ubuntu, Windows, Kali)
2. Splunk inputs/outputs configuration (in `configs/splunk/`)
3. Sysmon config (SwiftOnSecurity-derived) in `configs/sysmon/`
4. Detection rules (SPL), YAML rule stubs, mapping to MITRE ATT&CK in `detections/`
5. Dashboards & queries in `dashboards/`
6. Runbook / triage playbooks in `docs/runbook/`
7. Project documentation and demo screenshots in `proofs/`

## Getting started (quick)
1. Clone repo:
   ```bash
   git clone git@github.com:DeCyberGuardian/splunk-soc-lab.git
   cd splunk-soc-lab
>>>>>>> 617a5ce3fc64520d006e76769eb7643d3976a582

## Repository Structure Overview

This project is organized into the following directories to maintain clear documentation and component separation.

| Folder | Purpose |
| :--- | :--- |
| **📘 `docs/`** | Lab documentation, setup guides, architecture notes, and environment breakdowns. |
| **🗺️ `lab-diagrams/`** | Visual network topology, VM architecture, and log flow diagrams to explain how data moves through the lab. |
| **⚙️ `configs/`** | Configurations for Sysmon, Splunk Forwarder, Winlogbeat, Linux auditd, and other log sources needed for detection engineering. |
| **🛡️ `detection-rules/`** | SPL searches and Elastic Query DSL rules mapped to MITRE ATT&CK techniques, including tuning notes and detection logic. |
| **🧰 `scripts/`** | Helper tools (log generators, Linux monitoring scripts, attacker automation, etc.) to support repeatable testing. |
| **🚨 `attack-scenarios/`** | Realistic simulations such as brute force, lateral movement, privilege escalation, and persistence techniques. |
| **📑 `playbooks/`** | SOC-style investigation guides, triage workflows, and recommended response steps mapped to alerts. |
| **🖼️ `screenshots/`** | Evidence, dashboards, detections, and lab results used for documentation and portfolio presentation. |
