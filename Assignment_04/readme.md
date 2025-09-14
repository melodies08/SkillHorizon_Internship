# Active Reconnaissance Report: `testfire.net`

This report details the findings from a controlled, active reconnaissance scan conducted on the authorized target `testfire.net`. The objective was to discover live hosts, open ports, running services, and web application directories as per the assignment requirements.

-----

# 1. Host Discovery Results

A preliminary Nmap ping scan was conducted to verify that the host was online and to identify its IP address.

  * **Target Hostname:** `testfire.net`
  * **Resolved IP Address:** `65.61.137.117`
  * **Status:** The host was confirmed to be **UP** and responsive.

-----

# 2. Nmap Outputs

Several Nmap scans were performed to build a detailed profile of the target machine.

#### **Initial TCP SYN Scan (`-sS`)**

This scan quickly identified the open ports on the target.

```
Nmap scan report for testfire.net (65.61.137.117)
Host is up (0.027s latency).
Not shown: 997 filtered tcp ports (no-response)
PORT     STATE SERVICE
80/tcp   open  http
443/tcp  open  https
8080/tcp open  http-proxy
```

#### **Service & Version Scan (`-sV -sC`)**

This scan was run on all ports to identify service versions and run default scripts.

```
Nmap scan report for testfire.net (65.61.137.117)
Host is up (0.0042s latency).
Not shown: 65532 filtered tcp ports (no-response)
PORT     STATE SERVICE  VERSION
80/tcp   open  http     Apache Tomcat/Coyote JSP engine 1.1
|_http-server-header: Apache-Coyote/1.1
|_http-title: Altoro Mutual
443/tcp  open  ssl/http Apache Tomcat/Coyote JSP engine 1.1
| ssl-cert: Subject: commonName=demo.testfire.net
8080/tcp open  http     Apache Tomcat/Coyote JSP engine 1.1
|_http-title: Altoro Mutual
```

#### **OS Detection Scan (`-O`)**

This scan attempted to identify the operating system of the target.

```
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Aggressive OS guesses: Actiontec MI424WR-GEN3I WAP (97%), DD-WRT v24-sp2 (Linux 2.4.37) (97%), ...
No exact OS matches for host (test conditions non-ideal).
```

-----

# 3. Open Ports & Services

Based on the full port scan, the following ports and services were identified:

| Port | State | Service | Version Information |
| :--- | :--- | :--- | :--- |
| 80/tcp | open | http | Apache Tomcat/Coyote JSP engine 1.1 |
| 443/tcp | open | ssl/http | Apache Tomcat/Coyote JSP engine 1.1 |
| 8080/tcp | open | http | Apache Tomcat/Coyote JSP engine 1.1 |
| 22/tcp | filtered | ssh | N/A |

All other 65,531 ports were found to be in a `filtered` state, meaning a firewall or other network appliance is preventing Nmap from determining if they are open or closed.

-----

# 4. NSE Scripts Used and Findings

The `-sC` flag enabled the Nmap Scripting Engine (NSE) to run default scripts, which provided the following valuable information:

  * **`http-title`**: This script ran on ports 80 and 8080 and extracted the HTML title **"Altoro Mutual"**. This confirms the presence of a web application and gives it a name.
  * **`http-server-header`**: This script identified the server as **"Apache-Coyote/1.1"** on all open web ports, which is characteristic of an Apache Tomcat server used for Java applications.
  * **`ssl-cert`**: On port 443, this script parsed the SSL certificate. It revealed that the certificate's Common Name is for `demo.testfire.net`, uncovering a related subdomain.

-----

# 5. HTTP Enumeration Results (Dirb)

The `dirb` tool was used with the `common.txt` wordlist to discover directories and files on the web server.

  * **Key Discovered Paths:**
      * `/admin` (Responds with 302 Redirect, confirming its existence)
      * `/bank` (Responds with 302 Redirect, likely a core application area)
      * `/images` (Responds with 302 Redirect)
      * `/static` (Responds with 302 Redirect)
      * `/util` (Responds with 302 Redirect)
      * `/aux`, `/con`, `/prn`, `/nul`: Discovery of these Windows reserved filenames is noteworthy.

-----

# 6. Web Fingerprinting (WhatWeb & Nikto)

#### **WhatWeb**

The `whatweb` tool provided a quick summary of the web technologies in use.

  * **Identified Technologies:** Apache, Java, Apache-Coyote/1.1, `JSESSIONID` Cookies.
  * **IP/Country:** Confirmed the IP as `65.61.137.117` in the United States.

#### **Nikto**

The `nikto` scan identified several potential security issues and misconfigurations:

  * **Missing Headers:** The `X-Frame-Options` and `X-Content-Type-Options` headers are not set, which could expose the site to clickjacking and MIME-type sniffing attacks.
  * **Allowed HTTP Methods:** The server's `Allow` header indicates that potentially dangerous methods like **`PUT`** and **`DELETE`** are enabled, which could allow for unauthorized file modification or deletion if not properly restricted.
  * **Junk Method Response:** The server provided a valid response to junk HTTP methods, suggesting it may not be optimally configured to handle unexpected requests.
