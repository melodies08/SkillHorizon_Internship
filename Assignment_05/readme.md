# Automated Vulnerability Scanning Report

### 🎯 Objective
The objective of this assignment was to perform a safe and legal vulnerability scan of the web application **`testphp.vulnweb.com`**. The process involved initial reconnaissance, running multiple scanners, interpreting the results, and summarizing the findings in a professional report.

---
## 1. Reconnaissance & Discovery Summary
Before scanning, an initial reconnaissance phase was conducted to understand the target's footprint.

* **Host & Service Discovery:** The target `testphp.vulnweb.com` was found to be **UP** at the IP address `44.228.249.3`. The rDNS record revealed it is hosted on **Amazon AWS**. An Nmap scan showed that only port **80 (HTTP)** was open, running **nginx 1.19.0**.
* **Web Technology Fingerprinting:** A `whatweb` scan confirmed the server is `nginx/1.19.0` and identified the backend programming language as **PHP version 5.6.40**. It also discovered an email address (`wvs@acunetix.com`) and the application's title, "Home of Acunetix Art".
* **Directory Enumeration:** A `gobuster` scan discovered several interesting paths. The most critical finding was an exposed **`/CVS/`** version control directory, which could lead to source code disclosure. Other directories like `/admin/`, `/secured/`, and `/vendor/` were also identified.

---
## 2. Automated Vulnerability Scan Results
A series of automated scanners were used to identify vulnerabilities, moving from light checks to more aggressive scanning.

#### **Nikto Scan**
The Nikto scanner identified several server misconfigurations and security issues:
* **Missing Security Headers:** Confirmed the absence of `X-Frame-Options` and `X-Content-Type-Options` headers.
* **Information Disclosure:** The `X-Powered-By` header revealed the specific PHP version in use.
* **Insecure Policy Files:** Found `clientaccesspolicy.xml` and `crossdomain.xml` files with insecure wildcard entries, which can allow unintended cross-domain data access.

#### **Nuclei Scan**
The Nuclei scanner used template-based checks to find a variety of issues, corroborating and expanding on Nikto's findings:
* **Extensive Missing Headers:** Nuclei identified a comprehensive list of over 10 missing security headers, including `Content-Security-Policy`, `Strict-Transport-Security`, and `Permissions-Policy`.
* **Potential Information Exposure:** A template matched a possible exposure of `.idea/workspace.xml`, a file associated with the JetBrains IDE that could leak project information.

#### **OWASP ZAP Scan**
A full automated (active) scan was run using OWASP ZAP, which uncovered several critical vulnerabilities by sending malicious payloads.
* **High-Risk Findings:** ZAP identified multiple instances of **SQL Injection** and **Cross-Site Scripting (Reflected and DOM-based)**, representing the most severe risks found.
* **Medium-Risk Findings:** The scan also reported **Application Error Disclosure** (leaking path information), **Missing Anti-CSRF Tokens** in forms, and confirmed the lack of a **Content Security Policy (CSP)**.

#### **WPScan**
To check for a specific application type, WPScan was run against the target.
* **Result:** The scan quickly and correctly determined that the target **is not a WordPress site** and aborted.

---
## 3. Summary of Key Vulnerabilities

The combined results from all scanners paint a clear picture of the application's security posture. The most significant vulnerabilities are summarized below.

| Vulnerability | Risk Level | Description | Tool(s) |
| :--- | :--- | :--- | :--- |
| **SQL Injection** | **High** | The application is vulnerable to SQL injection, allowing an attacker to potentially access or manipulate the database. | OWASP ZAP |
| **Cross-Site Scripting (XSS)**| **High** | Reflected and DOM-based XSS were found. This allows an attacker to execute malicious scripts in a victim's browser, which can lead to session hijacking. | OWASP ZAP |
| **Insecure Security Headers** | **Medium** | Missing headers like CSP and X-Frame-Options expose users to attacks such as clickjacking and other client-side attacks. | OWASP ZAP, Nikto, Nuclei |
| **Information Disclosure** | **Low/Medium** | The exposed `/CVS/` directory, verbose application errors, and detailed server/PHP version headers provide an attacker with valuable system information. | Gobuster, OWASP ZAP, Nikto, WhatWeb |

---
## 4. Conclusion & Recommendations

The automated scans were highly effective at identifying critical vulnerabilities in `testphp.vulnweb.com`. The application has a poor security posture and contains multiple high-risk flaws that would be trivial for an attacker to exploit.

The following remediation steps are recommended:

1.  **Prioritize High-Risk Flaws:** Immediately address the **SQL Injection** and **XSS** vulnerabilities. This should be done by implementing parameterized database queries (prepared statements) and applying context-aware output encoding on all user-supplied data.
2.  **Harden Server Configuration:**
    * Implement a strict **Content Security Policy (CSP)** and other security headers (`X-Frame-Options`, `X-Content-Type-Options`, `Strict-Transport-Security`).
    * Configure the web server to **suppress version information** in `Server` and `X-Powered-By` headers.
3.  **Remediate Information Leaks:** The exposed **`/CVS/` directory should be removed** or firewalled from public access immediately to prevent source code leakage. Custom error pages should be implemented to prevent application errors from disclosing sensitive information.
