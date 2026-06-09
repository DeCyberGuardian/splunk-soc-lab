# 🛡️ Splunk SOC Lab — Log Analysis, Detection Engineering & Alerting

**Author:** DeCyberGuardian

A SOC-style home lab that ingests Windows (Sysmon + Event Logs) and Linux telemetry into Splunk, then builds detections, dashboards, and triage playbooks mapped to MITRE ATT&CK. The point is to practise the full detection-engineering loop: generate real attack telemetry, catch it, alert on it, and write the runbook for the analyst who picks the alert up.

## 🧱 Architecture

| Host | Role |
| :--- | :--- |
| Ubuntu VM | Splunk Enterprise (Indexer + Search Head) |
| Windows 11 VM | Endpoint — Sysmon + Splunk Universal Forwarder |
| Kali VM | Attacker / telemetry generator |

**Data flow**

```
Windows Events & Sysmon ─┐
                         ├─> Splunk UF ─> Splunk Indexer (index=sysmon, winevent, linux)
Linux logs ──────────────┘
```

## 📂 Repository structure

| Folder | What's in it |
| :--- | :--- |
| `docs/` | Setup guides, architecture notes, environment breakdown |
| `lab-diagrams/` | Network topology, VM layout, and log-flow diagrams |
| `configs/` | Sysmon (SwiftOnSecurity-derived), Splunk forwarder, and Linux auditd configs |
| `detection-rules/` | SPL searches mapped to MITRE ATT&CK, with tuning notes |
| `scripts/` | Log generators and attacker-automation helpers for repeatable testing |
| `attack-scenarios/` | Brute force, lateral movement, privilege escalation, persistence |
| `playbooks/` | Triage workflows and response steps mapped to alerts |
| `screenshots/` | Dashboards, detections, and lab results |

## 🚀 Getting started

```bash
git clone https://github.com/DeCyberGuardian/splunk-soc-lab.git
cd splunk-soc-lab
```

Then follow `docs/` to stand up Splunk, point the forwarders at the indexer, and load the Sysmon config. Once telemetry is flowing, run a scenario from `attack-scenarios/` and watch the matching rule in `detection-rules/` fire.

## 🎯 What this lab delivers

- Reproducible build steps for the Ubuntu / Windows / Kali stack
- Splunk inputs/outputs and Sysmon configuration
- ATT&CK-mapped SPL detections with tuning notes
- Dashboards and SOC triage playbooks
- Screenshots as proof of detections firing

## 🧠 Notes from building it

- Detections are only as good as the telemetry under them — getting Sysmon configured correctly mattered more than the rule logic itself.
- Writing the triage playbook alongside each detection forced me to think like the analyst receiving the alert, not just the engineer writing it.
