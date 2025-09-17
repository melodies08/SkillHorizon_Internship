# Step 2: Light Automated Scans

**Objective:** To use a variety of automated scanners to perform initial vulnerability discovery on the target application, identifying misconfigurations, common vulnerabilities, and missing security controls.

**Target:** `http://testphp.vulnweb.com`

-----

## 1. Nikto Scan

Nikto was used to check for common web server misconfigurations and outdated software.

  * **Command:** `nikto -h http://testphp.vulnweb.com -o nikto_testphp.txt`
  * **Key Findings:**
      * **Missing Security Headers:** The scan confirmed the absence of the `X-Frame-Options` and `X-Content-Type-Options` headers.
      * **Information Disclosure:** The server version (`nginx/1.19.0`) and backend technology (`PHP/5.6.40-38...`) were identified via HTTP headers.
      * **Insecure Policies:** Found `clientaccesspolicy.xml` and `crossdomain.xml` files with full wildcard entries, which can be insecure.

-----

## 2. Nuclei Scan

Nuclei was run with its default templates to perform fast checks for known vulnerabilities and misconfigurations.

  * **Command:** `nuclei -u http://testphp.vulnweb.com -o nuclei_testphp.txt -c 10`
  * **Key Findings:**
      * **Extensive Missing Headers:** Nuclei identified a comprehensive list of missing security headers, including `Content-Security-Policy`, `Strict-Transport-Security`, and `Permissions-Policy`.
      * **Technology Detection:** Confirmed the use of `nginx` and `PHP`.
      * **Potential Exposure:** Detected a template for a possible `.idea/workspace.xml` file exposure, which could leak development information.

-----

## 3. OWASP ZAP Scan

An automated scan was performed using OWASP ZAP to actively test for a wide range of web application vulnerabilities.

  * **Scan Type:** Full Automated Scan.
  * **Key Findings:** The scan identified a total of **18 alerts**, ranging from High to Informational.
      * **High Risk:** The most critical findings include multiple instances of **Cross-Site Scripting (Reflected and DOM-based)** and **SQL Injection**.
      * **Medium Risk:** The application was found to have **Missing Anti-CSRF Tokens**, **Application Error Disclosure**, and is missing a **Content Security Policy (CSP)**.
      * **Low Risk:** The scan confirmed information leakage via the `X-Powered-By` and `Server` headers.

-----

## 4. WPScan

A scan was run to determine if the target was a WordPress site.

  * **Command:** `wpscan --url http://testphp.vulnweb.com`
  * **Result:** The scan was aborted because the remote website **does not appear to be running WordPress**. This successfully rules out WordPress-specific vulnerabilities.
