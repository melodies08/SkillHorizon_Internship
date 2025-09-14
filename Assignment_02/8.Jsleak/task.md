# Task 8: Search for Secrets in JS Files

**Objective:** To analyze the collected JavaScript file for hardcoded secrets such as API keys, tokens, or hidden endpoints.

-----

### 🛠️ Tool Used

  - `JSleak`

-----

### 📝 Findings

The single JavaScript file identified in the previous task, `jquery-1.8.1.min.js`, was analyzed using `JSleak` to scan for potential secrets.

**Command Executed:**
`cat js_urls.txt | jsleak -s -l -c 20 -k`

**Result of the Scan:**
The scan completed, but **no hardcoded secrets** like API keys, passwords, or sensitive tokens were discovered in the JavaScript file.

The output shows that `jsleak`'s link-finding module identified several strings related to content types (e.g., `text/xml`, `text/html`) within the jQuery file. It then tested these strings as potential endpoints, which returned a `200 OK` status. However, this is a normal function of the tool and does not indicate an information leak or vulnerability.
