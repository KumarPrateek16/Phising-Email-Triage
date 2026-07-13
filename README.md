# Phishing Email Triage & Incident Analysis

## 🎯 Project Objective
The goal of this project is to simulate the daily responsibilities of a Security Operations Center (SOC) Tier 1 Analyst. This repository demonstrates the safe handling, analysis, and documentation of multiple malicious phishing emails. By investigating email headers, defanging Indicators of Compromise (IoCs), and utilizing Open-Source Intelligence (OSINT) tools, this project highlights key threat hunting and incident response skills across various attack vectors.

## 🛠️ Tools & Technologies Used
* **Virtualization / Sandboxing:** VmWare Workstation Pro [Isolated Environment - (Kali Linux)]
* **Phishing Email Dataset / Source:** Kaggle, Malware-Traffic-Analysis.net
* **OSINT & Threat Intelligence:** VirusTotal, urlscan.io, Cisco Talos
* **Data Decoding:** CyberChef
* **Documentation:** Markdown, GitHub

## 📂 Repository Structure
```text
phishing-email-triage/
├── README.md                           # Project overview and methodology
├── artifacts/
│   └── Analysis/                   # Artifacts for the Apple phishing sample
│        ├── raw_email_artifact.txt      # Raw extracted email data
│        ├── raw_email_headers.txt       # Extracted and sanitized email headers
│        ├── virustotal_analysis.png     # VirusTotal vendor scores (Screenshot)
│        └── virustotal_analysis.txt     # VirusTotal Report summary
└── report/
    └── Report-Apple-Lure.md                   # Final SOC triage ticket for Apple sample
```



## 📝 Scenario Overview
**Context:** The SOC routinely receives user-reported emails flagged as suspicious. These campaigns masquerade as trusted entities (such as major tech brands, corporate IT, or financial institutions), utilizing urgency and threats of account suspension to deceive users into compromising their credentials.
**Task:** Analyze multiple raw email data files across different campaigns, safely extract artifacts, determine the true nature of the threats, and draft comprehensive incident reports with actionable mitigation steps for each scenario.

## 🔍 Investigation Methodology

### 1. Header Analysis
* Analyzed the Received, From, and Return-Path fields to determine the true sender origins.
* Checked Domain-based Message Authentication, Reporting, and Conformance (DMARC), Sender Policy Framework (SPF), and DomainKeys Identified Mail (DKIM) records. (Result: Failed/Spoofed).

### 2. Payload Extraction & Defanging
* Identified the embedded Call-to-Action (CTA) hyperlinks within the email bodies.
* Defanged the URLs to prevent accidental execution (e.g., converted http://malicious-login-site.com to hxxp[://]malicious-login-site[.]com).

### 3. Open-Source Intelligence (OSINT) Verification
* Submitted the defanged URLs to urlscan.io to safely capture the site's DOM and screenshots without exposing the local network.
* Queried VirusTotal with the senders' IP addresses and extracted domains to determine reputation scores and historical malicious activity.

## 🛡️ Key Findings & Containment Recommendations
* **Threat Type:** Credential Harvesting (Phishing), Social Engineering
* **Spoofed Entities:** Various (e.g., Apple Store / iTunes Security, Corporate IT Support)
* **Recommended Actions:**
  1. **Block:** Add the extracted malicious domains and sender IPs to the corporate firewall and web proxy blocklists.
  2. **Purge:** Run an enterprise-wide mail trace to identify any other recipients of these campaigns and soft-delete the emails from their inboxes.
  3. **Remediate:** Force a password reset and revoke active session tokens for any users who interacted with the malicious links.

---
*Disclaimer: All artifacts and indicators in this repository are defanged and utilized strictly for educational and portfolio demonstration purposes.*

