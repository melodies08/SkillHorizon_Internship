# Passive Reconnaissance Report

### 🎯 1. Target Domain Name Chosen

The target domain selected for this passive reconnaissance assignment is **`hackthissite.org`**.

***

### 🌐 2. WHOIS & DNS Findings

Analysis of the domain's registration and DNS records provided foundational infrastructure details.

* **WHOIS Data:** The domain is registered with **Porkbun LLC**. It was first created on **August 10, 2003**, with a current registration expiry date of August 10, 2026. Most contact details for the registrant and administrator have been redacted for privacy.
* **DNS Records:** The domain resolves to multiple A records, suggesting **load balancing**. Mail exchange (MX) records point to Google's servers. The domain has strong security configurations, including SPF records to prevent email spoofing and CAA records that restrict certificate issuance to specific authorities like Let's Encrypt and Sectigo.

***

### 📂 3. Subdomains Discovered

Through various enumeration techniques, the following subdomains and related domains were identified:

* `www.hackthissite.org`
* `mirror.hackthissite.org`
* `data.htscdn.org` (CDN for static assets)
* `irc.hackthissite.org`
* `legal.hackthissite.org`
* `qdb.hackthissite.org`
* `hts.io` (A related domain)

***

### 📧 4. Email IDs or Employee Data

The reconnaissance for publicly available contact information yielded limited results.

* **Email IDs:** No specific employee email addresses were discovered. The only email address found was `admin@hackthissite.org`, which was identified from the SOA record in the DNS findings.
* **Employee Data:** No specific employee names, roles, or profiles were found through automated tools or manual searches on platforms like LinkedIn.

***

### 📄 5. Metadata Information

A search for public documents was conducted to analyze for potentially sensitive metadata.

* **Result:** The `metagoofil` tool was used to scan for `.pdf`, `.docx`, and `.pptx` files associated with the domain. The scan completed but **found no documents** to download. Therefore, no metadata could be extracted.

***

### 🔎 6. Google Dorks Attempted

Advanced Google Dorking queries were used to find indexed information that might not be readily visible.

* `site:hackthissite.org filetype:pdf`: This query successfully located **18 PDF files**, which were mostly community magazines or "zines".
* `site:hackthissite.org inurl:login`: This query identified **multiple login pages** and user registration links, which are key entry points to the application.
* `site:hackthissite.org intitle:"index of"`: This query **returned no results**, indicating that no open web directories were indexed by Google.

***

### 🕵️ 7. OSINT Summary

Open Source Intelligence gathering focused on the target's presence on public platforms.

* **GitHub:** A search on GitHub revealed **12 public repositories** under the "hackthissite" topic. These are primarily solution writeups for the site's challenges, indicating an active user community.
* **Maltego:** A Maltego graph was generated to visualize the domain's infrastructure. It successfully mapped the relationships between the domain, its registrar (Porkbun LLC), its name servers, and other public WHOIS data, confirming earlier findings.
* **Social Media:** The target maintains a community presence on platforms like Twitter, Facebook, and Discord, with links found on its main page.

***

### 🔗 8. URLs & Leak Data in JS Files (Updated)

The website's endpoints were collected and analyzed to identify technologies and potential information leaks.

* **URL Collection:** A comprehensive list of URLs was collected, revealing the site's structure, various mission pages, forum links, and an official **Tor onion service**.
* **JS File Analysis:** The site uses only one primary JavaScript file: `https://data.htscdn.org/js/jquery-1.8.1.min.js`. This file was scanned with the `jsleak` tool to find any hardcoded secrets (API keys, credentials). **The scan found no secrets**. The tool's output only showed some content-type strings as links, which is not a vulnerability.

***

### 💡 9. Conclusion: Possible Attack Surfaces

Based on the information gathered through passive reconnaissance, several potential attack surfaces were identified:

1.  **Outdated Software:** The use of **jQuery version 1.8.1** is a significant finding. This version is outdated and has multiple known vulnerabilities (CVEs) that could potentially be exploited, primarily for Cross-Site Scripting (XSS) attacks.
2.  **Exposed Login Interfaces:** The discovery of multiple login and password reset pages provides clear targets for brute-force, credential stuffing, and user enumeration attacks.
3.  **Community-Sourced Intelligence:** The public GitHub repositories with challenge solutions, while not a direct flaw, could be reverse-engineered to understand the application's logic and potentially discover vulnerabilities in older, unpatched parts of the site.
