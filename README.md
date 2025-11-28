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

## SSH Screenshots

### SSH 1
![SSH Screenshot 1](./screenshots/ssh_1.png)

### SSH 2
![SSH Screenshot 2](./screenshots/ssh_2.png)

### SSH 3
![SSH Screenshot 3](./screenshots/ssh_3.png)

### SSH 4
![SSH Screenshot 4](./screenshots/ssh_4.png)

### SSH 5
![SSH Screenshot 5](./screenshots/ssh_5.png)

### SSH 6
![SSH Screenshot 6](./screenshots/ssh_6.png)

