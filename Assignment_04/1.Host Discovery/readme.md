# Step 1: Host Discovery

**Objective:** To confirm if the target host is online and resolve its IP address using a ping scan.

**Target:** `testfire.net`

-----

### Command Used

```bash
nmap -sn testfire.net
```

-----

### Findings

```
Starting Nmap 7.95 ( https://nmap.org ) at 2025-09-14 16:36 IST
Nmap scan report for testfire.net (65.61.137.117)
Host is up (0.00073s latency).
Nmap done: 1 IP address (1 host up) scanned in 1.52 seconds
```

**Summary:**

  * **Status:** The host is **UP**.
  * **IP Address:** `65.61.137.117`.
