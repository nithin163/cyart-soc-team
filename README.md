# cyart-soc-team
Below is a GitHub‑ready `README.md` that documents all five practical application parts in a clean, professional format. You can copy‑paste this into your repo and adjust any details (dates, IPs, screenshots) after you run the labs.

***

# Mini SOC – Alert Management and Incident Response Labs

This repository documents a series of hands‑on labs extending a mini Security Operations Center (SOC) environment with practical alert management, incident response documentation, triage, evidence preservation, and a full alert‑to‑response capstone workflow based on Wazuh, Metasploit, and supporting tools. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/81451689/74b0fca5-00d9-456f-9823-113fe43476ee/Parimi-Nithin-kumar-weekly-task.pdf)

***

## 1. Alert Management Practice

### 1.1 Objectives

- Design an alert classification system in Google Sheets.  
- Map alerts to MITRE ATT&CK techniques and assign priorities.  
- Practice prioritizing alerts using CVSS scores and business context.  
- Create and document incident tickets in TheHive and practice escalation.  

### 1.2 Tools

- Google Sheets  
- Wazuh  
- TheHive  

### 1.3 Alert Classification System

In Google Sheets, create a table to classify alerts and map them to MITRE ATT&CK:

```text
| Alert ID | Type           | Priority | MITRE Technique |
|----------|----------------|----------|-----------------|
| 001      | Phishing Email | High     | T1566           |
| 002      | Brute-force SSH| Medium   | T1110           |
| 003      | Ransomware     | Critical | T1486           |
| 004      | Port Scan      | Low      | T1046           |
```

Example test alert:  
- “Phishing Email: Suspicious Link” → Alert ID `001`, Type `Phishing`, Priority `High`, Technique `T1566`.

> Placeholders for screenshots:  
> - `screenshots/alert-classification-sheet.png` (Google Sheets view)  
> - `screenshots/wazuh-priority-dashboard.png` (Wazuh priority pie chart)  

### 1.4 Prioritizing Alerts with CVSS

Simulate alerts and assign priority using CVSS and asset criticality:

```text
| Alert ID | Description                         | CVSS | Asset Criticality | Priority  |
|----------|-------------------------------------|------|-------------------|----------|
| 005      | Log4Shell Exploit Detected         | 9.8  | Internet-facing   | Critical |
| 006      | Ransomware Activity on File Server | 9.1  | High              | Critical |
| 007      | Suspicious Script on Low-value VM  | 5.5  | Low               | Medium   |
| 008      | Simple Port Scan from External IP  | 2.0  | Medium            | Low      |
```

Guidelines:  
- CVSS 9.0–10.0 on critical assets → Critical.  
- High CVSS on non‑critical assets or medium CVSS on critical assets → High/Medium based on context.  

### 1.5 Wazuh Priority Dashboard

Configure a Wazuh / Kibana dashboard to visualize the distribution of alert priorities (e.g., pie chart of Critical / High / Medium / Low). Use your existing Mini‑SOC dashboards as a reference. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/81451689/74b0fca5-00d9-456f-9823-113fe43476ee/Parimi-Nithin-kumar-weekly-task.pdf)

Suggested panels:  
- Pie chart: alerts by `rule.level` or custom priority field.  
- Bar chart: top 10 alert types.  

### 1.6 TheHive Incident Ticket Example

Sample ticket for a Critical alert:

```text
Title: [Critical] Ransomware Detected on Server-X

Description:
A ransomware pattern was detected on Server-X with multiple files being encrypted in a short time window.
Indicators:
- File: crypto_locker.exe
- Host: SERVER-X
- Source IP: 192.168.1.50
- Suspicious extensions: .locked

Priority: Critical
Assignee: SOC Analyst
Status: Open
Tags: ransomware, high-impact, server-x
```

> Placeholder: `screenshots/thehive-ticket-ransomware.png`

### 1.7 Escalation Email (Tier 1 → Tier 2)

Example ~100‑word escalation email:

> Subject: Escalation – [Critical] Ransomware Detected on Server‑X  
>   
> Hi Tier‑2 Team,  
>   
> A Critical alert was triggered on Server‑X for suspected ransomware activity. Wazuh detected rapid file modifications and an unknown executable named `crypto_locker.exe` originating from 192.168.1.50. Initial triage confirms abnormal encryption patterns on a production file share. I have isolated the host from the network and opened an incident in TheHive with all current IOCs and logs attached.  
>   
> Please review for deeper analysis and containment recommendations.  
>   
> Regards,  
> Tier‑1 SOC Analyst  

***

## 2. Response Documentation

### 2.1 Objectives

- Build an incident response template similar to SANS style.  
- Document investigation timelines and actions.  
- Create a reusable phishing incident checklist.  
- Perform a brief post‑mortem focused on process improvements.  

### 2.2 Tools

- Google Docs  
- Draw.io (for diagrams and timelines)  

### 2.3 Incident Response Template (Mock Phishing)

Create a Google Doc template with sections:

1. **Executive Summary**  
   One‑paragraph overview of the incident, affected users, and high‑level impact.  

2. **Timeline**  
   Key timestamps and actions taken.  

   ```text
   | Timestamp           | Action                       |
   |---------------------|------------------------------|
   | 2025-08-18 13:45:00 | Phishing email received      |
   | 2025-08-18 14:00:00 | Isolated endpoint            |
   | 2025-08-18 14:30:00 | Collected memory dump        |
   | 2025-08-18 15:00:00 | Reset affected user password |
   ```

3. **Impact Analysis**  
   - Number of affected users.  
   - Any credential exposure.  
   - Business or regulatory implications.  

4. **Remediation Steps**  
   - Blocking malicious domains/URLs.  
   - User password resets.  
   - Email filtering rule updates.  

5. **Lessons Learned**  
   - Gaps in training, tools, or process.  
   - Required improvements to detection or response.  

> Placeholder: `diagrams/phishing-ir-flow.drawio` (Draw.io flowchart)

### 2.4 Investigation Steps Log

Use a simple actions table for each mock incident:

```text
| Timestamp            | Action                           |
|----------------------|----------------------------------|
| 2025-08-18 14:00:00 | Isolated endpoint from network   |
| 2025-08-18 14:30:00 | Collected memory dump            |
| 2025-08-18 15:00:00 | Pulled email headers for analysis|
| 2025-08-18 15:30:00 | Checked link on VirusTotal       |
| 2025-08-18 16:00:00 | Identified affected users        |
```

### 2.5 Phishing Checklist

Create a reusable checklist in Google Docs:

```text
[ ] Confirm email headers (sender, SPF/DKIM/DMARC)
[ ] Verify sender domain and reply-to address
[ ] Analyze URLs (hover, expand, check for lookalikes)
[ ] Check link/file reputation in VirusTotal
[ ] Identify and list all recipients and affected users
[ ] Collect relevant logs (mail, proxy, endpoint)
[ ] Reset passwords if credentials may be compromised
[ ] Block malicious domains/URLs and update filters
[ ] Notify users with security awareness guidance
[ ] Document incident in IR template and close ticket
```

### 2.6 Post‑Mortem Summary (50 words)

Example:

> The phishing simulation exposed delays in identifying affected users and gaps in email header analysis. Introducing a standardized checklist, improving user awareness training, and integrating URL reputation checks into the workflow will streamline triage. Updating email filtering rules and playbooks will reduce future response times and misclassification.  

***

## 3. Alert Triage Practice

### 3.1 Objectives

- Perform structured triage on sample alerts in Wazuh.  
- Distinguish true positives from false positives using context and threat intel.  
- Document triage decisions and status.  

### 3.2 Tools

- Wazuh  
- VirusTotal  
- AlienVault OTX  

### 3.3 Triage Simulation Table

Example mock alert in Wazuh:

```text
| Alert ID | Description        | Source IP      | Priority | Status |
|----------|--------------------|----------------|----------|--------|
| 002      | Brute-force SSH    | 192.168.1.100  | Medium   | Open   |
| 009      | Suspicious Binary  | 10.0.0.25      | High     | Open   |
```

Triage steps for `Alert ID 002` (Brute‑force SSH):  
- Check login success after failures.  
- Confirm whether SSH is exposed to the internet.  
- Review asset importance of target system.  

### 3.4 Threat Intelligence Validation

For each IP or hash:  
- Query VirusTotal and AlienVault OTX.  
- Note whether the IOC is known malicious, benign, or unknown.  

Example 50‑word summary:

> The brute‑force SSH alert from 192.168.1.100 was linked to an internal lab attacker system, and threat intelligence checks showed no external malicious reputation. After confirming no successful logins and that the target was a low‑risk test VM, the event was marked as a controlled lab simulation and closed as non‑malicious.  

***

## 4. Evidence Preservation

### 4.1 Objectives

- Practice collecting volatile and non‑volatile evidence.  
- Hash evidence and document it in a chain‑of‑custody style table.  

### 4.2 Tools

- Velociraptor  
- FTK Imager  
- `sha256sum` (or equivalent hashing tool)  

### 4.3 Volatile Data Collection

From a Windows VM, using Velociraptor:

- Collect active network connections:

  ```sql
  SELECT * FROM netstat;
  ```

- Export results to CSV: `netstat-YYYYMMDD.csv`.  

> Placeholder: `evidence/netstat-YYYYMMDD.csv`  

### 4.4 Memory Dump and Hashing

- Use Velociraptor artifact (conceptually): `Artifact.Windows.Memory.Acquisition`.  
- Save memory dump as `server-x-memdump.raw`.  
- Compute hash:

  ```bash
  sha256sum server-x-memdump.raw > server-x-memdump.sha256
  ```

### 4.5 Evidence Documentation Table

```text
| Item        | Description        | Collected By | Date       | Hash Value        |
|-------------|--------------------|--------------|------------|-------------------|
| Memory Dump | Server-X Dump      | SOC Analyst  | 2025-08-18 | <SHA256>          |
| Netstat CSV | Active connections | SOC Analyst  | 2025-08-18 | <SHA256>          |
```

Guidelines:  
- Store evidence and hash files in `evidence/` folder.  
- Do not modify original evidence after hashing; work on copies.  

***

## 5. Capstone Project – Full Alert‑to‑Response Cycle

### 5.1 Objectives

- Simulate a real attack using Metasploit.  
- Detect and triage the attack using Wazuh.  
- Respond by isolating the host and blocking the attacker IP with CrowdSec.  
- Document the incident with both technical and non‑technical reports.  

### 5.2 Tools

- Metasploit  
- Wazuh  
- CrowdSec (or similar IP blocking mechanism)  
- Google Docs  

### 5.3 Attack Simulation

1. Launch `msfconsole` on the attacker system.  
2. Use the VSFTPD backdoor exploit against Metasploitable2:

   ```bash
   use exploit/unix/ftp/vsftpd_234_backdoor
   set RHOSTS <metasploitable2-ip>
   set RPORT 21
   run
   ```

3. Confirm that a shell session is opened.  

> Placeholder: `screenshots/metasploit-vsftpd-exploit.png`  

### 5.4 Detection and Triage in Wazuh

Ensure Wazuh is receiving logs from the Metasploitable2 host. Configure rules or correlation to identify the exploit attempt. Document the alert:

```text
| Timestamp            | Source IP      | Alert Description   | MITRE Technique |
|----------------------|----------------|---------------------|-----------------|
| 2025-08-18 11:00:00 | 192.168.1.100  | VSFTPD exploit      | T1190           |
```

Triage checks:  
- Confirm exploit success (session created).  
- Verify asset role (test vs. production).  
- Decide to escalate as an incident.  

> Placeholder: `screenshots/wazuh-vsftpd-alert.png`  

### 5.5 Response with CrowdSec

- Isolate the vulnerable VM (host‑only or internal network only).  
- Block attacker IP with CrowdSec/firewall rule.  
- Validate using `ping` or another connection test from attacker to victim.  

Example conceptual command:

```bash
# Example firewall style (may vary by environment)
sudo iptables -A INPUT -s 192.168.1.100 -j DROP
```

### 5.6 Technical Incident Report (~200 words)

Use a SANS‑style template in Google Docs:

Sections:  
1. Executive Summary  
2. Timeline  
3. Impact Assessment  
4. Containment & Eradication  
5. Recommendations  

Example (adapt/shorten as needed):

> On 2025‑08‑18 at 11:00, the SOC detected an exploit attempt against the VSFTPD service on the Metasploitable2 lab host. Wazuh generated a high‑severity alert indicating suspicious FTP activity originating from 192.168.1.100. Metasploit logs confirmed use of the `vsftpd_234_backdoor` exploit module, resulting in a remote shell session on the target system.  
>  
> During detection and analysis, the event was mapped to MITRE ATT&CK technique T1190 (Exploit Public‑Facing Application). As part of containment, the Metasploitable2 VM was isolated from the main lab network, and the attacker IP was blocked using CrowdSec/firewall rules. Eradication was performed by reverting the vulnerable VM to a known‑good snapshot and restricting external access to the VSFTPD service.  
>  
> In the recovery phase, normal connectivity was restored while additional Wazuh rules were implemented to flag similar exploit signatures. The incident highlighted the importance of timely patching, asset inventory of exposed services, and continuous monitoring. Recommended improvements include hardening lab services, tightening network segmentation, and refining alerts for exploitation attempts.  

### 5.7 Stakeholder Briefing (Non‑Technical, ~100 words)

> This exercise simulated an attack against a vulnerable FTP service on a test server in our lab. An attacker system successfully exploited the service and gained remote access. Our monitoring tools detected the activity, and the security team quickly isolated the affected server and blocked the attacker’s IP address. No real business data was at risk because the environment was fully controlled for training purposes. The scenario demonstrated that our detection and response processes are effective and also revealed areas to improve patching and network controls on exposed services, which will further reduce the risk of similar attacks.  

***

## 6. Repository Structure

Suggested directory layout:

```text
.
├── README.md                      # This file
├── sheets/                        # Alert classification, CVSS scoring
├── docs/                          # IR templates, phishing reports, capstone report
├── diagrams/                      # Draw.io flows
├── evidence/                      # Memory dumps, CSVs, hashes (lab only)
├── screenshots/                   # Wazuh, TheHive, Metasploit, dashboards
└── scripts/                       # Optional helper scripts / notes
```

***

## 7. How to Use This Repo

1. Clone the repo into your lab environment.  
2. Run each lab step‑by‑step and capture screenshots.  
3. Fill the Google Sheets and Docs templates based on your actual alerts and incidents.  
4. Export or attach completed documents and place them into the `docs/` directory.  
5. Keep sensitive or real‑world data out of the repository; use only lab‑generated data.
