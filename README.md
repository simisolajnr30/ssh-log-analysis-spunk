SSH Log Analysis Using Splunk

This project focuses on analyzing SSH logs to check failed logins, repeated attempts, successful logins, and SSH connections without authentication.

Tools Used:

Splunk

Steps Performed:

1. Search and return only SSH logs, group them by event type, and count how many SSH logs exist in each event_type

index=ssh_logs | stats count by event_type


2. Search inside SSH logs, return only failed login, group events by source IP and count how many times each IP failed to login

index=ssh_logs event_type="Failed SSH Login" | stats count by id.orig_h


3. Search inside SSH logs, return only logs with repeated failed attempts, group by source and destination IP, and count how many times the source IP tried and failed to log into that destination IP

index=ssh_logs event_type="Multiple Failed Authentication Attempts" | stats count by id.orig_h id.resp_h


4. Search inside SSH logs, return only successful SSH login events, group events by source IP, and count how many times each IP successfully logged into the destination IP

index=ssh_logs event_type="Successful SSH Login" | stats count by id.orig_h id.resp_h


5. Search inside SSH logs, return only SSH logs with connections without authentication, group events by source IP, and count how many times each IP connected without logging in

index=ssh_logs event_type="Connection Without Authentication" | stats count by id.orig_h


6. Search inside SSH logs, return only SSH connections without authentication and show a timechart of how each source IP’s unauthorized connections change over time

index=ssh_logs event_type="Connection Without Authentication" | timechart count by id.orig_h
