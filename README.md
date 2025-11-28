# SSH Log Analysis using Splunk

This project focuses on analyzing SSH logs to identify failed logins, repeated authentication attempts, successful logins, and connections made without authentication.

---

## **Tools Used**
- Splunk

---

## **Steps Performed**

- Uploaded the sample SSH log to Splunk.

- Searched for SSH events

```splunk
index=ssh_logs | stats count by event_type
```

- Searched for failed SSH login attempts

```splunk
index=ssh_logs event_type="Failed SSH Login" 
| stats count by id.orig_h
```

- Identified repeated failed authentication attempts

```splunk
index=ssh_logs event_type="Multiple Failed Authentication Attempts" 
| stats count by id.orig_h id.resp_h
```

- Searched for successful SSH login events

```splunk
index=ssh_logs event_type="Successful SSH Login" 
| stats count by id.orig_h id.resp_h
```

- Listed SSH connections without authentication

```splunk
index=ssh_logs event_type="Connection Without Authentication" 
| stats count by id.orig_h
```

- Visualized unauthorized SSH connections over time

```splunk
index=ssh_logs event_type="Connection Without Authentication" 
| timechart count by id.orig_h
```

---
![SSH 1](screenshot/ssh/ssh-1.png)
![SSH 2](screenshot/ssh/ssh-2.png)
![SSH 3](screenshot/ssh/ssh-3.png)
![SSH 4](screenshot/ssh/ssh-4.png)
![SSH 5](screenshot/ssh/ssh-5.png)
![SSH 6](screenshot/ssh/ssh-6.png)
