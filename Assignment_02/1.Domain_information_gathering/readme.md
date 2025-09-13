# Task 1: Domain Information Gathering

**Objective:** To gather publicly available domain registration and DNS information about the target using `whois`, `dig`, and `nslookup`.

[cite\_start]**Target Domain:** `hackthissite.org` [cite: 68]

-----

### 🛠️ Tools Used

  - `whois`
  - `dig`
  - `nslookup`

-----

### 📝 Findings

#### 1\. WHOIS Lookup

The `whois` command provided the following registration details for the domain:

```
Domain Name: hackthissite.org
Registry Domain ID: REDACTED
Registrar WHOIS Server: http://whois.porkbun.com
Registrar URL: https://porkbun.com
Updated Date: 2025-07-15T23:08:30Z
Creation Date: 2003-08-10T15:01:25Z
Registry Expiry Date: 2026-08-10T15:01:25Z
Registrar: Porkbun LLC
Name Server: c.ns.buddyns.com
Name Server: f.ns.buddyns.com
Name Server: g.ns.buddyns.com
Name Server: h.ns.buddyns.com
Name Server: j.ns.buddyns.com
```

*(Full output redacted for brevity)*

**Key Information Gathered:**

  - [cite\_start]**Registrar:** Porkbun LLC [cite: 68]
  - [cite\_start]**Creation Date:** 2003-08-10 [cite: 68]
  - [cite\_start]**Expiration Date:** 2026-08-10 [cite: 68]
  - [cite\_start]**Registrant Contact Info:** Redacted for Privacy (Data Protected) [cite: 68]
  - [cite\_start]**Name Servers:** `c.ns.buddyns.com`, `f.ns.buddyns.com`, `g.ns.buddyns.com`, `h.ns.buddyns.com`, `j.ns.buddyns.com` [cite: 69]

#### 2\. DNS Records (dig / nslookup)

DNS queries using `dig` and `nslookup` revealed the following key records:

```
;; ANSWER SECTION:
hackthissite.org.	3090	IN	NS	c.ns.buddyns.com.
hackthissite.org.	3090	IN	NS	f.ns.buddyns.com.
hackthissite.org.	3090	IN	NS	g.ns.buddyns.com.
hackthissite.org.	3090	IN	NS	h.ns.buddyns.com.
hackthissite.org.	3090	IN	NS	j.ns.buddyns.com.
hackthissite.org.	3090	IN	A	137.74.187.100
hackthissite.org.	3090	IN	A	137.74.187.101
hackthissite.org.	3090	IN	A	137.74.187.102
hackthissite.org.	3090	IN	A	137.74.187.103
hackthissite.org.	3090	IN	A	137.74.187.104
hackthissite.org.	3090	IN	MX	10 aspmx.l.google.com.
hackthissite.org.	3090	IN	MX	20 alt1.aspmx.l.google.com.
hackthissite.org.	3090	IN	MX	20 alt2.aspmx.l.google.com.
hackthissite.org.	3090	IN	SOA	c.ns.buddyns.com. admin.hackthissite.org. 2025032501 3600 900 1209600 3600
```

*(Full output redacted for brevity)*

**Key Records Found:**

  - [cite\_start]**A Records (IPv4 Addresses):** The domain resolves to multiple IP addresses: `137.74.187.100`, `137.74.187.101`, `137.74.187.102`, `137.74.187.103`, and `137.74.187.104`[cite: 4, 10]. This suggests load balancing.
  - [cite\_start]**MX Records (Mail Servers):** Mail services are handled by Google, with servers like `aspmx.l.google.com`[cite: 7].
  - [cite\_start]**NS Records (Name Servers):** The authoritative name servers are provided by `buddyns.com`[cite: 4].
  - [cite\_start]**SOA Record (Start of Authority):** The primary name server is `c.ns.buddyns.com` and the administrative contact email is `admin.hackthissite.org`[cite: 7].
  - [cite\_start]**TXT Records:** An SPF record is configured to prevent email spoofing, authorizing Google and specific IPs[cite: 4].
  - [cite\_start]**CAA Records:** The domain has explicitly authorized `letsencrypt.org`, `sectigo.com`, and `harica.gr` as certificate authorities, enhancing security by restricting who can issue SSL/TLS certificates for the domain[cite: 5, 6].


**nslookup Command Output:**
