# Project Overview

This project focuses on HTTP traffic analysis using Splunk Enterprise and a dataset containing over 2 million HTTP log events.

The investigation included:

- HTTP traffic analysis
- Web attack detection
- Directory enumeration analysis
- Directory traversal investigation
- Time-based traffic analysis
- Dashboard creation
- Suspicious IP investigation and correlation

The HTTP dataset was imported into a custom Splunk lab environment for analysis and investigation.

---

## Technologies Used

- Splunk Enterprise
- SPL (Search Processing Language)
- VMware Workstation
- Ubuntu Server (Splunk Server)
- Windows 11 VM
- Web log dataset (HTTP access logs)

---

## Dataset Information

| Item | Value |
|---|---|
| Data Type | HTTP Access Logs |
| Total Events | 2,048,440 |
| Source Type | http_logs |
| Splunk Index | soc-splunk-lab |

---

## Key Analysis Performed

- Total HTTP event analysis
- HTTP request method analysis
- HTTP status code distribution
- Top requested URIs
- Top source IP analysis
- HTTP traffic analysis over time
- 404 response analysis
- Suspicious IP investigation
- Directory enumeration detection
- Directory traversal detection
- User-Agent analysis

---

## Dashboards

The following dashboards were created during the investigation:

- HTTP Traffic Over Time
- Top Source IP Addresses
- HTTP Status Code Distribution
- HTTP Methods Distribution
- Top Requested URIs
- Top Source IPs (404 Analysis)

---


## Project Structure

http-log-analysis/
│
├── Dashboards/
├── screenshots/
├── README.md
├── findings.md
├── investigation-notes.md
└── spl-queries.md
