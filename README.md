# splunk-security-dashboard

## Overview
This project demonstrates a Splunk-based security monitoring dashboard for tracking failed authentication attempts. Built as part of a hands-on lab to secure monitoring and alerting 
## Features
- **Real-time Monitoring**: Tracks failed login attempts by source IP over time
- **Top Offenders View**: Identifies IP address with the highest number of failed attempts
- **Threshold-Based Alerting**: Automatically triggers alerts when a single IP exceeds 5 failed attempts in 5 minutes

## Dashboard Panels
1. **Failed Login Attempts by Source IP** - Line chart showing failure trends over time
2. **Top 10 Attacking IP Addresses** - Table ranked by total failure count
3. **Total Failed Login Attempts** - Single value showing overall failure volume

## Alert Rule
- **Condition**: > 5 failed logins from single IP in 5 minutes
- **Action**: Email notification
- **Use case**: Rapid detection of brute force or credential stuffing attacks
## Technologies Used
- Splunk
- SPL
- Window Event Logs (4625)
## Key SPL Searches 
### Time-based visualization 
```text
index=* (tag=authentication action=failure) OR (sourcetype="XmlWinEventLog:Security" EventCode=4625)) | timechart count by src_ip
```
### Top offenders 
```
index=* (tag=authentication action=failure) OR (sourcetype="XmlWinEventLog:Security" EventCode=4625)) | stats count by src_ip | sort - count | head 10
```
## Screenshots
