# Wireshark Investigation - Identifying Infected Host 

## Objective 
To analyze newtork traffic using wireshark and identify a potentitally infected windows based on suspicious activity.

## Methodology 

- Analyzed a network traffic from a packet a packet capture file
- Changd the time format to UTC Date and Time of Day
- Applied DNS filters to observe domain queries
- Identified unusual repeated DNS requests
- Traced suspicious traffic back to the source IP
- Extracted systems details including MAC address, hostname, and user information by applying specific filters

  ## Findings

  - **Suspicious Domoain:**
    'wpad.easyas123.tech'
  - **Infected Machine IP Address:**
    '10.2.28.88
  - **MAC Address:**
    '00:19:d1:b2:4d:ad'
  - **Hostname:**
    'DESKTOP-TEYQ2NR'
  - **User Account Name:**
    'brolf'
  - **Full Name:**
    'Becka Rolf'

## Analysis 

The infected host was identified by observing repeated DNS queries to a suspicious domain ('wpad.easyas123.tech'). This pattern suggests possible malicious activity, such as malware beaconing to an external server. By filtering and analyzing tghe traffic, I traced the activity back to the source IP and extracteed key system details including the MAC address, hostname and associated user account.

## SOC Perspective 

From a SOC analyst standpoint, this type of activity could be detected through: 

- Monitoring unusual DNS traffic patterns
- Identifying repeated queries to unknown or suspicious domains
- Investigating endpoints generating abnormal network behaviour

Early detection of such activity can help prevent further compromise or data exfiltration.

## What I learned 

- How to use Wireshark to analyze network traffic
- How to identify suspicious DNS behaviour
- How to trace network activity back to a specific host
- The importance of traffic analysis in detecting compromised systems
