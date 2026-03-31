## Scenario
Analyzed Windows Security logs to investigate repeated failed login attempts suggesting a possible brute force attack targeting a local account.

## Investigation Approach
- Filtered logs for failed login events (Event ID 4625)
- Identified repeated authentication failures against a specific account
- Analyzed failure reasons to understand the nature of the login attempts
- Observed source IP and connection behaviour
- Reviewed source port activity to identify patterns consistent with automated attacks
- Performed WHOIS lookup on the identified source IP address to gather additional context such as geographic location and ownership information

## Key Observations 
- Multiple failed login attempts were recorded within a short period
- A single account was cosistently targeted across the events
- Failure reason indicated incorrect credentials during authentication
- Activity originated from an external IP address
- Source ports varied across attempts, indicating automated connection attempts
- External lookup of the source IP provided additional context regarding its origin and potential legitimacy

## Analysis 
The pattern of repeated failed login attempts targeting a single account, combined with varying source ports and consistent failure reasons, strongly indicates a brute force attack.
This behaviour is typical of automated tools attempting multiple password combinations until successful access is achieved

## Recommended Actions 
- Temporarily lock of monitor the targeted account
- Implement account lockout policies after multiple failed attempts
- Restrict RDP access where possible
- Monitor for any successful login following the failed attempts
- Investigate source IP reputation using threat intelligence tools

## Conclusion
The activity observed in the logs aligns with a brute force attack targeting a local account through repeated authentication attempts. Identifying such patterns is critical in early detection and response within a SOC environment.
