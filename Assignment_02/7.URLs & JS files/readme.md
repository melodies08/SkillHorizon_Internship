# Task 7: Collect URLs and Filter for JS Files

**Objective:** To crawl and collect all accessible URLs from the target domain and then filter this list to isolate JavaScript (`.js`) files for further analysis.

**Target Domain:** `hackthissite.org`

-----

### 🛠️ Tools Used

  - `linkfinder` (or another URL extraction tool)
  - `grep`

-----

### 📝 Findings

#### 1\. URL & Endpoint Collection

A URL extraction tool was used to gather a comprehensive list of links and endpoints from the target domain. The scan discovered a wide range of paths, including internal pages, mission links, user functions, and external partner links.

**Sample of Discovered URLs:**

```
/user/login
/register
/missions/basic/
/forums
http://hackthisjogneh42n5o7gbzrewxee3vyu6ex37ukyvdw6jm66npakiyd.onion/
https://data.htscdn.org/js/jquery-1.8.1.min.js
```

#### 2\. JavaScript File Filtering

The list of discovered URLs was then filtered to isolate only the JavaScript files for focused analysis.

**Command Executed:**
`grep -Ei '\.js([?#]|$)' linkfinder_hackthissite.txt | sort -u > js_urls.txt`

**Result:**
The filtering process identified only **one unique JavaScript file** being used by the web application.

  - `https://data.htscdn.org/js/jquery-1.8.1.min.js`

