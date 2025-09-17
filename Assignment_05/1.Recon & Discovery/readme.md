# Step 1: Recon & Discovery

**Objective:** To perform initial reconnaissance on the target to identify if it's live, what services are running, what web technologies are in use, and to discover common web directories.

**Target:** `testphp.vulnweb.com`

-----

## 1. Nmap Scan (Host & Service Discovery)

An Nmap scan was run against the top 1000 ports to identify running services.

  * **Command:** `nmap --top-ports 1000 -sV --open testphp.vulnweb.com`
  * **Results:**
      * **Host Status:** The host is **UP**.
      * **IP Address:** `44.228.249.3`.
      * **rDNS Record:** `ec2-44-228-249-3.us-west-2.compute.amazonaws.com`, indicating the server is hosted on Amazon AWS.
      * **Open Ports:** Only port **80/tcp** was found to be open.
      * **Service Version:** The service on port 80 is **nginx 1.19.0**.

-----

## 2. WhatWeb Fingerprinting

The `whatweb` tool was used to identify the specific technologies used by the web application.

  * **Command:** `whatweb http://testphp.vulnweb.com`
  * **Identified Technologies:**
      * **Web Server:** `nginx/1.19.0`.
      * **Programming Language:** `PHP/5.6.40`.
      * **Other:** Adobe Flash, an email address (`wvs@acunetix.com`), and the title "Home of Acunetix Art" were also identified.

-----

## 3. Gobuster Directory Discovery

The `gobuster` tool was used with the `common.txt` wordlist to find common directories and files.

  * **Command:** `gobuster dir -u http://testphp.vulnweb.com -w /usr/share/wordlists/dirb/common.txt`
  * **Key Discovered Paths:**
      * `/admin/` (Status: 301 - Redirects, confirming its existence).
      * `/cgi-bin/` (Status: 403 - Forbidden).
      * `/CVS/`: An exposed Concurrent Versions System directory was found, containing `Entries`, `Repository`, and `Root` files (Status: 200), which could leak source code information.
      * `/images/`, `/pictures/`, `/secured/`, `/vendor/`: Other directories were identified via 301 redirects.
