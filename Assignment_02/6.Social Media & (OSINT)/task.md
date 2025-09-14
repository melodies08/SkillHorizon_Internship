# Task 6: Social Media & Open Source Intelligence (OSINT)

**Objective:** To identify the target's presence on social media platforms and gather intelligence using OSINT tools.

**Target:** `hackthissite.org`

-----

### 🛠️ Tools Used

  - `Maltego (CE)`
  - Manual searching on public platforms (GitHub)

-----

### 📝 OSINT Summary

#### Maltego Analysis

Using Maltego, a graph of the target domain's infrastructure was generated. The tool successfully mapped the relationships between the core domain and its associated entities.

  - **Key Findings:** The graph visually confirmed the information gathered in earlier tasks, linking `hackthissite.org` to its **registrar** (Porkbun LLC), **name servers** (https://www.google.com/search?q=ns.buddyns.com), and publicly listed **contact information** (abuse@porkbun.com). This provides a clear, high-level overview of the target's public-facing DNS and registration footprint.

#### GitHub

A search on GitHub for the topic "hackthissite" was performed to find any related code repositories.

  - **Key Findings:** The search revealed **12 public repositories**. These repositories primarily contain user-submitted solution writeups and code for the challenges on the website. While this indicates an active community, no repositories belonging to an official organization account or containing the site's source code were found.

#### Other Platforms (LinkedIn, Twitter)

A manual search on major social media platforms like LinkedIn and Twitter did not reveal any official pages for the organization. This is expected, as HackThisSite is a non-commercial, educational platform rather than a corporate entity.
