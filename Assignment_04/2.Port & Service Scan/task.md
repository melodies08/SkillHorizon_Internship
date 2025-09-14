# Step 2: Port & Service Scan (Nmap)

**Objective:** To identify open ports, running services, version information, and potential OS details using various Nmap scans.

**Target:** `testfire.net`

-----

### Scans Performed & Findings

#### 1\. Quick TCP SYN Scan (`-sS`)

  * **Command:** `nmap -sS testfire.net`

  * **Results:**

    ```
    PORT     STATE SERVICE
    80/tcp   open  http
    443/tcp  open  https
    8080/tcp open  http-proxy
    ```

  * **Summary:** The initial scan found three open TCP ports: 80, 443, and 8080. 997 other scanned ports were in a filtered state.

#### 2\. Service & Version Scan (`-sV -sC`)

  * **Command:** `nmap -sV -p 22,80,443 -sC testfire.net`
  * **Summary of Findings:**
      * **Port 80 (HTTP):** Running Apache Tomcat/Coyote JSP engine 1.1. The `http-title` script found the page title "Altoro Mutual".
      * **Port 443 (HTTPS):** Also running Apache Tomcat/Coyote JSP engine 1.1. The `ssl-cert` script showed the certificate is for `demo.testfire.net`.
      * **Port 22 (SSH):** This port was found to be `filtered`, meaning it did not respond.

#### 3\. Full Port Scan with Scripts (`-p 1-65535 -sC`)

  * **Command:** `nmap -sV -p 1-65535 -sC testfire.net`
  * **Summary:** A scan of all 65,535 ports confirmed that only ports 80, 443, and 8080 are open. No other open ports were discovered. All three open ports are running the same Apache Tomcat/Coyote JSP engine 1.1 service.

#### 4\. Operating System (OS) Detection (`-O`)

  * **Command:** `nmap -O --osscan-guess testfire.net`
  * **Summary:** Nmap could not determine an exact OS match because test conditions were non-ideal. However, its aggressive guesses included various Linux kernels and Microsoft Windows versions (XP, 7, Server 2012).
