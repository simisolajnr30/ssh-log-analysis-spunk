🔐 SSH Log Analysis Using Splunk

A cybersecurity project focused on SSH authentication analysis using Splunk.
This project shows how to analyze failed logins, repeated login attempts, successful logins, and SSH connections without authentication.

🎯 Objective

To analyze SSH logs and provide visibility into authentication activity, detect possible brute-force attacks, and track unauthorized access attempts.

🛠 Tools Used

1. Splunk Enterprise
2. SSH Logs Dataset (ssh_logs)

Steps Performed
1. search and return only ssh logs, group them by event type and count how many ssh logs exist in each event_type
index=ssh_logs
| stats count by event_type

2. search inside ssh logs, return only failed login, group events by src IP and count how many times each IP failed to login
index=ssh_logs event_type="Failed SSH Login"
| stats count by id.orig_h

3. search inside ssh logs, return only logs with repeated failed attempts, group by source and destination ip, and count how many times the src ip tried and failed to log into that destination ip
index=ssh_logs event_type="Multiple Failed Authentication Attempts"
| stats count by id.orig_h id.resp_h

4. search inside ssh logs, return only successful ssh login events, group events by src ip and count how many times each ip successfully login into the destination ip
index=ssh_logs event_type="Successful SSH Login"
| stats count by id.orig_h id.resp_h

5. search inside ssh logs, return only ssh logs with connections without authentication, group events by src ip, and count how many times each ip connected without logging in
index=ssh_logs event_type="Connection Without Authentication"
| stats count by id.orig_h

6. search inside ssh logs, return only ssh connections without authentication and show timechart of how each source ips unauthorized connections change overtime
index=ssh_logs event_type="Connection Without Authentication"
| timechart count by id.orig_h
