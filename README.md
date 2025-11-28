🔐 SSH Log Analysis

A cybersecurity project focused on SSH authentication analysis using Splunk.
This project shows how to visualize failed logins, detect repeated login attempts, successful logins, and connections without authentication.

🎯 Objective

To analyze SSH logs and provide visibility into authentication activity, possible brute-force attempts, and unauthorized access attempts.

🛠 Tools Used

Splunk

SSH Logs Dataset

⚙️ Steps Performed
1️⃣ Search all SSH logs by event type
index=ssh_logs
| stats count by event_type

2️⃣ Search failed SSH logins by source IP
index=ssh_logs event_type="Failed SSH Login"
| stats count by id.orig_h

3️⃣ Search repeated failed attempts by source and destination IP
index=ssh_logs event_type="Multiple Failed Authentication Attempts"
| stats count by id.orig_h id.resp_h

4️⃣ Search successful logins by source and destination IP
index=ssh_logs event_type="Successful SSH Login"
| stats count by id.orig_h id.resp_h

5️⃣ Search SSH connections without authentication by source IP
index=ssh_logs event_type="Connection Without Authentication"
| stats count by id.orig_h

6️⃣ Timechart of unauthorized connections by source IP
index=ssh_logs event_type="Connection Without Authentication"
| timechart count by id.orig_h
