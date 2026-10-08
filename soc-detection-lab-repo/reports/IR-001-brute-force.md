# Incident Report

**Report ID:** IR-2026-001
**Date/Time Detected:** [fill in from your Dashboard]
**Analyst:** [your name]
**Severity:** Medium
**Status:** Closed

## Summary
Repeated SSH authentication failures detected against soc-endpoint
(172.18.0.5) within a short time window, triggering custom correlation
rule 100010.

## Affected Host(s) / User(s)
- Host: soc-endpoint (172.18.0.5)
- User: labuser

## Timeline
| Time | Event |
|---|---|
| [time] | First auth failure logged |
| [time] | 6th auth failure, custom rule 100010 fired |

## Indicators of Compromise (IOCs)
| Type | Value | Enrichment Result |
|---|---|---|
| Source IP | [your host's Docker network IP] | Internal lab IP — no external enrichment needed |

## Detection Source
Rule ID: 100010
Rule Description: Possible brute force: 5+ SSH auth failures in 60 seconds
MITRE ATT&CK Mapping: T1110 — Brute Force

## Investigation Notes
Confirmed via Threat Hunting search `rule.id:100010` that the rule
correctly correlated 6 failed SSH login attempts against user labuser
within the 60-second detection window. Cross-referenced with base rule
5716 (sshd authentication failure) to confirm each individual event.

## Verdict
True Positive (lab-simulated) — deliberately triggered test matching
the exact pattern the rule was designed to catch.

## Containment / Remediation Actions
- In a real environment: block source IP at firewall, temporarily lock
  the targeted account, review for any successful logins from the same source

## Recommendations
- Consider lowering the frequency threshold for production environments
  with stricter brute-force tolerance
- Add automated active-response to block the source IP after rule 100010 fires
