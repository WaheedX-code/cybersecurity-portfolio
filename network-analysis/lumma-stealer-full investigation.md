# Wireshark Investigation - Luma Stealer Malware Analysis
## Objective 
To analyze a PCAP file using Wireshark and identify signs of Lumma Stealer malware infection, trace command-and-control (C2)communication, and extract relevant indicators of compromise(IOCs).

## Methodology
- Analyzed PCAP file using Wireshark
- Applied filters: DNS, HTTP, Kerberos, TCP
- Identified suspicious domains and traffic patterns
- Investigated HTTP requests and responses
- Followed TCP streams to inspect potential exfiltration
- Extracted host and user information

## Infected Host Details
- **IP Address:** '10.1.21.58'
- **MAC Address:** '00:21:5d:c8:0e:f2'
- **Hostname:** 'DESKTOP-ES9F3ML'
- **User Account:** 'gwyatt'
- **Full Name:** 'Gabriel Wyatt'

## Findings
- **Malicious Domain:** 'whitepepper.su'
- **C2 IP Address:** '153.92.1.49

- Suspicious request to :
   - '/favicon.ico'
   - '/api/set_agent'
     
- Observed:
   - Repeated communication with C2 server
   - Suspicious HTTP POST request
   - Encrypted communication over port 443

 ## Indicators of Compromise (IOCs)
  - Domain: 'whitepepper.su'
  - IP: '153.92.1.49'
  - URIs:
     - '/favicon.ico'
     - '/api/set_agent'

## Analysis 
Duriing the investigation, I observed repeated communication between the infected host and a suspicious external domain ('whitepepper.su').
A key indicator was the request to 'favicon.ico'. After further research, I learned that Lumma Stealer uses this request as a connectivity check before initiating data exfiltration.
I also identified a suspicious HTTP POST request to '/api/set_agent'. By following the TCP stream, I was able to observe potential data being transmitted from the infected system.
These behaviors strongly indicate Lumma Stealer activity and possible data exfiltration.

## SOC Perspective 
This type of activity could be detected through:

- Monitoring DNS queries to suspicious domains
- Detecting repeated outbond communication patterns
- Identifying unusual HTTP requests
- Investigating abnormal POST requests
- Correlating traffic with known malicious infrastructure

## What I Learned 
- How to identify Lumma Stealer behavior through network traffic
- Importance of analyzing small anomalies (e.g. favicon.ico requests)
- How to use TCP stream analysis to detect exfiltration
- How attackers use simple techniques to blend malicious traffic with normal activity

## Evidence
