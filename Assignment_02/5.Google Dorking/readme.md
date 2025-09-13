# Task 5: Google Dorking

**Objective:** To use advanced Google search queries (dorks) to find sensitive information, exposed documents, and indexed pages that are not meant for public viewing.

**Target Domain:** `hackthissite.org`

-----

### 🛠️ Method Used

  - Google Advanced Search Operators (Google Dorking)

-----

### 📝 Dorks Attempted & Results

The following table summarizes the Google Dorks used and their findings:

| Dork Query | Purpose | Results / Findings |
| :--- | :--- | :--- |
| `site:hackthissite.org filetype:pdf` | Find all indexed PDF files. | **18 PDF files were found.** The results primarily consist of "zines" (magazines) and articles hosted on a mirror subdomain. |
| `site:hackthissite.org inurl:login OR inurl:admin` | Find login pages. | **Multiple login pages were identified.** The primary result was the main user login page for the website. |
| `site:hackthissite.org intitle:"index of"` | Look for open directory listings. | **No results were found.** This indicates that no publicly exposed directory listings were discovered using this dork. |

