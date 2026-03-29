# SOC Investigation - Phishing Email & Fake Webmail Login Page

## Analyst
Mubeen

## Source
Malware-Traffic-Analysis.net

## Category 
Phishing / Credential Harvesting

## Tools Used
- Wireshark
- Sublime Text
- VirusTotal
- AbuseIPDB

## Executive Summary
This investigation analyzed a phishing campaign delivering a fake webmail login page used for credential harvesting.
Email header analysis revealed spoofing through SPF failure, absence of DKIM, and implicit DMARC failure. Examination of the raw '.eml' file exposed encoded malicious links and explicit social engineering techniques.
Network traffic analysis confirmed credential exfiltration via HTTP POST requests, including repeated submissions triggered by phishing kit behaviour.
Additional indicators such as '/favicon.ico' connectivity checks and '/gen204' Google Analytics beacons revealed active attacker monitioring of victim interaction.
The attack aligns with MITRE ATT&CK techniques for phishing, credential harvesting, and abuse of legitimate services.

## Objective
- Analyze email headers and raw '.eml' content
- Identify phishing infrastructure
- Trace credentials harvesting activity in network traffic
- Extract Indicators of Compromise (IOCs)
- Map activity to MITRE ATT&CK

## Phase ! - Email Header Analysis 
### Key Findings 
| Field | Value |
|------|-------|
| Sender | khz.port@scp.gov.iq |
| Relay Server | s940027.srvape.com |
| Sending IP | 188.127.242.252 |
| Subject | Account Validation!! For admin@malware-traffic-analysis.net Only!! |
### Observations
- **Domain mismatch:**
    Email claims to originate from a govrnment domain but is relayed through an unrelated hosting provider.
- **Authentication failures:**
   - SPF: Fail
   - DKIM: None
   - DMARC: Fail
- **Targeted social engineering:**
    Victim email embedded in subject line to increase credibility.

## Phase 1b - Raw Email (.eml) Analysis
### Quoted_Printable Encoding
- '=3D' decoded to '='
- Used to obscure malicious URLs from basic filters
### Page Spoofing
- Fake page mimics internal system
- Uses victim domain name to increase trust
### Social Engineering 
- Explicit requets for password
- Fake timestamp used to create urgency

## Phase 2 - Phishing Infrastructure Analysis 
### Malicious URL
hxxps://email.procedure[.]best/management.aspx?good=admin@malware-traffic-analysis[.]net
### Observations 
- **Phishing domain:** email.procedure[.]best
- **Credential harvesting parameter ('?good='):**
   - Pre-populates victim email
   - Reduces user friction and increases success rate
- **Infrastructure evasion:**
   - Hosted behind Cloudflare
   - Origin IP masked
   - Requires domain-level blocking

## Phase 3 - Network Traffic Analysis (Wireshark)
### Key Filters
http.host contains "procedure"
http.rquest.method == "POST"
http.request 
http.response

### Observed Traffic Flow
1. DNS request to phishing domain
2. TCP connection to Cloudflare IP
3. HTTP GET loads phishing page
4. Victim submits credentials
5. HTTP POST transmits credentials
6. Redirect occurs
7. Victim re-submits credentials

### Critical Findings
- **Victim IP:** 10.0.29.128
- **Phisihing Server IP:** 172.67.202.104 (Cloudflare)

### Behavioural Indicators 
- **Double credential POST**
 - Indicates phishing kit validation mechanism
- **/favicon.ico request**
 - Pre-submission connectivity check
- **/gen204 requests**
 - Google Analytics tracking
 - Real-time attacker notification
- **301 Redirects (Post Submission)**
 - Victim redirected to legitimate page
 - Encourages second credential submission

## TCP Stream Analysis - Credential Exfiltration
- Credentials observed in plaintext due to HTTP
- Direct confirmation of credential theft
> Note: In real-world HTTPS scenarios, TLS encryption would obscure payload, but SNI and proxy logs remain useful.

## Indicators of Compromise (IOCs)
| Type | Value |
|------|------|
| Sender Email | khz.port@scp[.]gov[.]iq |
| Sending IP | 188.127.242.252 |
| Victim Email | admin@malware-traffic-analysis[.]net |
| Phishing Domain | email.procedure[.]best |
| Phishing Server IP | 172.67.202.104 |
| Tracking IP | 142.250.115.113 |
| URL Parameter | ?good=admin@malware-traffic-analysis[.]net |

> Note: Indicators are defanged

## MITRE ATT&CK Mapping
| Tactic | Technique | ID |
|--------|-----------|-----|
| Initial Access | Phishing: Spearphishing Link | T1566.002 |
| Credential Access | Credentials Harvesting via Web Form | T1056 |
| Defense Evasion | Use of Legitimate Services (Cloudflare) | T1027 |
| Defense Evasion | Use of Legitimate Services (Google Analaytics) | T1102 |
| Reconnaissance | Victim Email in URL | T1598 |

## Attack Chain 
Phishing Email ->
Victim Clicks Link ->
Fake Login Page Loads ->
Credentials Submited ->
Tracking Signal sent ->
301 Redirect ->
Second Credential Submission ->
Credential Harvesting ->
Account Compromise 

## Detection Opportunities
| Layer | Detection |
|-------|---------|
| Email Gateway | SPF/DKIM/DMARC enforcement |
| DNS Monitoring | Suspicious domain detection | 
| Proxy/Web Filter | Detect credential pre-fill parameters |
| Network | Detect HTTP credentials POST |
| Endpoint | Browser warning |

## Impact 
- Credentials compromise
- Unauthorized access
- Potential lateral movement
- Data exposure

## Lessons Learned 
- Email authentication is critical for prevention
- Cloudflare masking requires domain-level blocking
- HTTP traffic exposes sensitive data
- URL parameters improve phishing success rate
- Google Analytics can be abused for attacker tracking
- Behavioural indicators (POST -> redirect -> POST) are strong detection signals

## Conclusions
This investigation demonstrates how phishing campaigns combine spoofed emails, social engineering, and credential harvesting infrastructure to compromise users.
It highlights the importance of behavioural analysis in detecting modern phishin gkits beyond simple IOC matching.

## References 
- Malware-Traffic-Analysis.net
- MITRE ATT&CK Framework


