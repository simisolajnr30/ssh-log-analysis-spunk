SSH Log Analysis using Splunk

This project focuses on analyzing SSH logs to check failed logins, repeated attempts, successful logins, and SSH connections without authentication.

Tools Used

Splunk

Steps Performed

search and return only ssh logs, group them by event type and count how many ssh logs exist in each event_type

index=ssh_logs
| stats count by event_type


search inside ssh logs, return only failed login, group events by src IP and count how many times each IP failed to login

index=ssh_logs event_type="Failed SSH Login"
| stats count by id.orig_h


search inside ssh logs, return only logs with repeated failed attempts, group by source and destination IP, and count how many times the src ip tried and failed to log into that destination ip

index=ssh_logs event_type="Multiple Failed Authentication Attempts"
| stats count by id.orig_h id.resp_h


search inside ssh logs, return only successful ssh login events, group events by src ip and count how many times each IP successfully login into the destination IP

index=ssh_logs event_type="Successful SSH Login"
| stats count by id.orig_h id.resp_h


search inside ssh logs, return only ssh logs with connections without authentication, group events by src ip, and count how many times each IP connected without logging in

index=ssh_logs event_type="Connection Without Authentication"
| stats count by id.orig_h


search inside ssh logs, return only ssh connections without authentication and show timechart of how each source IP’s unauthorized connections change over time

index=ssh_logs event_type="Connection Without Authentication"
| timechart count by id.orig_h
