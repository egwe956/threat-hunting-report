# Threat Hunting Report

## Overview
- Purpose: Document methodology, evidence, and conclusions from a threat hunt
- Scope: Network indicators, endpoint observations, log analysis, enrichment lookups
- Output: `threat_hunting_report.md` plus supporting images and logs

## Repository Structure
- `threat_hunting_report.md` — Main report with methodology, findings, and recommendations
- `dell_netstat_logs.jpg` — Network connections captured from endpoint review
- `reverseIPlookup.jpg`, `reverse_IP_lookup.jpg` — Reverse IP lookup evidence
- `mac_address_not_found.png` — MAC address anomaly evidence
- `post_method.png` — HTTP POST method observation
- `2_2.png`, `2.png` — Additional supporting artifacts and screenshots

## Methodology
1. Define hypothesis and hunting questions
2. Collect and normalize data from endpoints, firewall, and application logs
3. Enrich indicators with DNS, reverse lookup, and WHOIS
4. Correlate events across time and hosts
5. Validate findings, assess impact, recommend actions

## Key Artifacts
- Network connections snapshot
- Reverse IP results for suspicious hosts
- HTTP method analysis for possible exfiltration or command and control
- MAC lookup anomalies suggesting spoofing or incomplete asset inventory

## How To Use
1. Read `threat_hunting_report.md` end to end
2. Cross reference screenshots with timestamps and sections in the report
3. Re-run lookups and validations using the same indicators to confirm results
4. Apply recommendations in the Action Plan

## Reproduction Steps
- Reverse IP lookup
  - Use `nslookup`, `dig -x <ip>`, or third party intel sources
- Netstat style review
  - On Windows: `netstat -ano`, map PIDs to processes
  - On Linux or macOS: `ss -tunap` or `lsof -i`
- HTTP method inspection
  - Review proxy, WAF, or application logs for unusual POST patterns

## Findings Summary
- Suspicious external connections identified and validated
- Potential misconfiguration or spoofing indicated by MAC lookup gaps
- POST traffic patterns warrant deeper inspection for data movement

## Recommendations
- Blocklist or segment identified suspicious IPs and domains
- Enforce asset inventory reconciliation and MAC validation
- Enable enhanced HTTP logging and anomaly detection rules
- Add detections for unusual process to network behaviors
- Schedule periodic hunts with the same playbook for trend analysis
