# Task 4: Metadata Extraction

**Objective:** To download publicly available documents (PDF, DOCX, PPTX) from the target's domain and analyze them for hidden metadata.

**Target Domain:** `hackthissite.org`

-----

### 🛠️ Tool Used

  - `metagoofil`

-----

### 📝 Findings

The `metagoofil` tool was used to search for publicly indexed documents associated with the `hackthissite.org` domain.

**Command Executed:**
`metagoofil -d hackthissite.org -l 200 -n 200 -o /home/kali/SkillHorizon -t pdf,docx,pptx -w`

**Result:**
The scan completed successfully but **found no documents** matching the specified file types (pdf, docx, pptx). As no files could be downloaded, no metadata was extracted.
