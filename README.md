# SOC Detection & Incident Response Lab

A self-built, Docker-based SOC lab demonstrating detection engineering,
alert triage, and incident response using Wazuh. Monitors a Linux
endpoint via Wazuh Agent, auditd, and File Integrity Monitoring.

## What this demonstrates
- Deploying and troubleshooting a SIEM stack (Wazuh) in Docker
- Writing and testing custom detection rules
- Investigating alerts and mapping to MITRE ATT&CK
- Documenting incidents using a structured report format

## Architecture
Fully Docker-based — no VMs, no hypervisors. Wazuh Manager, Indexer,
and Dashboard run as separate containers, alongside a monitored Linux
endpoint container (soc-endpoint) running the Wazuh Agent, auditd, and
File Integrity Monitoring. All ports bound to 127.0.0.1 only — no
exposure beyond localhost. See docs/architecture.md for the full diagram.

## Scenarios Covered
- Brute force SSH login detection
- Obfuscated (base64) command execution
- Network reconnaissance (port scan)
- File integrity monitoring
- Synthetic phishing URL / IOC enrichment workflow

## Custom Rules
3 custom Wazuh rules in custom-rules/local_rules.xml:
- Rule 100010: Brute-force correlation (MITRE T1110)
- Rule 100011: Encoded command detection (MITRE T1140)
- Rule 100012: File integrity alert elevation (MITRE T1565)

## Incident Reports
See /reports for 4 completed write-ups, using the structured template
in IR-template.md.

## Disclaimer
Built entirely in an isolated, local Docker environment using only
systems I own. No real malware, credentials, or public targets involved.
This is a personal learning project, not production SOC experience.
