SSH Log Analysis Project (Splunk)

This project focuses on analyzing SSH activity using Splunk. I performed searches, grouped events, detected failed login patterns, brute-force attempts, successful logins, and suspicious unauthenticated connections. I also created visualizations like bar charts and timecharts.

🔍 1. Check SSH Logs and Group by Event Type

What I did:
I searched and returned only SSH logs, then grouped them by event_type to see how many logs exist in each category.

Query:

index=ssh_logs | stats count by event_type


❌ 2. Analyze Failed Login Attempts

What I did:
I searched inside the SSH logs and returned only failed login events. Then I grouped them by source IP and counted how many times each IP failed to log in.

Query:

index=ssh_logs event_type="Failed SSH Login"
| stats count by id.orig_h


🔁 3. Detect Repeated Failed Attempts (Brute Force)

What I did:
I returned only logs with repeated failed authentication attempts. Then I grouped them by source IP and destination IP to see how many times each source IP tried and failed to access the destination.

Query:

index=ssh_logs event_type="Multiple Failed Authentication Attempts"
| stats count by id.orig_h, id.resp_h


✅ 4. Track Successful SSH Logins

What I did:
I searched inside SSH logs and returned only successful login events. Then I grouped them by source IP to see how many times each IP successfully logged in.

Query:

index=ssh_logs event_type="Successful SSH Login"
| stats count by id.orig_h, id.resp_h


⚠️ 5. Spot Connections Without Authentication

What I did:
I searched inside SSH logs and returned only events where a connection happened without authentication. Then I grouped the results by source IP to count how many times each IP connected without logging in.

Query:

index=ssh_logs event_type="Connection Without Authentication"
| stats count by id.orig_h


📈 6. Timechart of Unauthorized Connections Over Time

What I did:
I created a timechart to visualize how these unauthorized connection attempts change over time.

Query:

index=ssh_logs event_type="Connection Without Authentication"
| timechart count by id.orig_h
