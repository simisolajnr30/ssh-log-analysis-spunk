SSH Log Analysis using Splunk

This project simulates analyzing SSH logs to identify failed login attempts, investigate brute-force behavior, track successful logins, and analyze unauthorized SSH connections.

Tools Used

Splunk

Steps Performed

Searched for SSH events

index=ssh_logs
| stats count by event_type


Returned only failed SSH logins and grouped them by source IP

index=ssh_logs event_type="Failed SSH Login"
| stats count by id.orig_h


Identified repeated failed attempts (possible brute-force) and grouped by source and destination IP

index=ssh_logs event_type="Multiple Failed Authentication Attempts"
| stats count by id.orig_h id.resp_h


Listed successful SSH login events and grouped them by source IP

index=ssh_logs event_type="Successful SSH Login"
| stats count by id.orig_h id.resp_h


Identified SSH connections without authentication and grouped by source IP

index=ssh_logs event_type="Connection Without Authentication"
| stats count by id.orig_h


Showed unauthorized SSH connections over time

index=ssh_logs event_type="Connection Without Authentication"
| timechart count by id.orig_h

