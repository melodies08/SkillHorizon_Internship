
# Assignment 02 – Passive Reconnaissance

## 🎯 Objective

Perform **passive footprinting and reconnaissance** of a web application using Kali Linux tools.
The goal is to gather publicly available information about the target without actively interacting with its systems. This is the **first phase of penetration testing**, helping to identify potential attack surfaces.

---

## 📝 Tasks Performed (Step-wise)

### 🔹 Step 1: Domain Information Gathering

* Tools: `whois`, `dig`, `nslookup`
* Collected domain registration details and DNS records.
* **Screenshots:**

  * ![WHOIS](./screenshots/whois.png)
  * ![DNS](./screenshots/dig.png)

---

### 🔹 Step 2: Subdomain Enumeration

* Tools: `subfinder`, `assetfinder`, `amass (passive mode)`
* Discovered subdomains of the target.
* **Screenshots:**

  * ![Subfinder](./screenshots/subfinder.png)
  * ![Assetfinder](./screenshots/assetfinder.png)
  * ![Amass](./screenshots/amass.png)

---

### 🔹 Step 3: Email & Employee Information

* Tool: `theHarvester`
* Gathered emails, names, and hosts from public sources (Google, Bing, LinkedIn, etc.).
* **Screenshot:** ![theHarvester](./screenshots/theharvester.png)

---

### 🔹 Step 4: Metadata Extraction

* Tools: `exiftool`, `strings`, `metagoofil`
* Extracted metadata from public documents (PDF, DOCX, PPTX).
* **Screenshot:** ![Metadata](./screenshots/metadata.png)

---

### 🔹 Step 5: Google Dorking

* Queries used:

  * `site:example.com filetype:pdf`
  * `site:example.com intitle:"index of"`
* **Screenshot:** ![GoogleDorking](./screenshots/dorking.png)

---

### 🔹 Step 6: OSINT – Social Media & Public Sources

* Tools: `Maltego (CE)`, `SpiderFoot`
* Checked for target presence on LinkedIn, Twitter, GitHub, etc.
* **Screenshot:** ![OSINT](./screenshots/osint.png)

---

### 🔹 Step 7: Collect URLs & Filter JS Files

* Tools: `gau`, `katana`, `linkfinder`
* Collected URLs of target and filtered JavaScript files.
* **Screenshot:** ![JSFiles](./screenshots/jsfiles.png)

---

### 🔹 Step 8: Search for Secrets in JS Files

* Tool: `JSleak`
* Identified possible secrets inside JS files.
* **Screenshot:** ![JSleak](./screenshots/jsleak.png)

---

## 📌 Deliverables

* Target domain name
* WHOIS & DNS findings
* Subdomains list
* Email IDs or employee data (if found)
* Metadata details with screenshots
* Google dorking results
* OSINT findings
* URL collection & JS leaks

---

## ✅ Conclusion

From the passive reconnaissance performed, possible attack surfaces were identified including:

* Publicly exposed subdomains
* Metadata leaks in documents
* Sensitive URLs and JavaScript files containing secrets
* Email IDs & employee data that can be leveraged in phishing/social engineering attacks

Nitin, kya tum chahte ho main tumhare liye **Assignment\_02 ka poora folder structure (task.md + screenshots folder)** bana kar zip de du, jise tum seedha GitHub pe upload kar sako?
