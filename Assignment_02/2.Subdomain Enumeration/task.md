# Task 2: Subdomain Enumeration

## Target
`hackthissite.org`

## Tools Used
- `subfinder`
- `assetfinder` 
- `amass` (passive mode)

## Commands
```bash
subfinder -d hackthissite.org | tee subfinder_hackthissite.txt
assetfinder hackthissite.org | tee assetfinder_hackthissite.txt
amass enum -passive -d hackthissite.org | tee amass_hackthissite.txt
```

## Key Findings

### Unique Subdomains Discovered (37 total)
- **Main Services:**
  - www.hackthissite.org
  - api.hackthissite.org
  - git.hackthissite.org
  - forums.hackthissite.org
  - mirror.hackthissite.org
  - stats.hackthissite.org
  - legal.hackthissite.org
  - staff.hackthissite.org

- **Development/Staging:**
  - v3dev.hackthissite.org
  - v3stage.hackthissite.org  
  - v3stage-cdn.hackthissite.org

- **IRC Network:**
  - irc.hackthissite.org
  - irc-hub.hackthissite.org
  - irc-v6.hackthissite.org
  - irc-ipv6.hackthissite.org
  - irc-wolf.hackthissite.org
  - irc-www.hackthissite.org
  - lille.irc.hackthissite.org
  - lille.irc-v6.hackthissite.org
  - wolf.irc.hackthissite.org
  - wolf.irc-v6.hackthissite.org
  - www.irc.hackthissite.org
  - new-irc.hackthissite.org

- **Infrastructure:**
  - vm-005.outbound.firewall.hackthissite.org
  - vm-050.outbound.firewall.hackthissite.org
  - vm-099.outbound.firewall.hackthissite.org
  - vm-150.outbound.firewall.hackthissite.org
  - vm-200.outbound.firewall.hackthissite.org

- **Other Services:**
  - mail.hackthissite.org
  - mta-sts.hackthissite.org
  - status.hackthissite.org
  - status-new.hackthissite.org
  - ctf.hackthissite.org
  - h5ai.hackthissite.org
  - qdb.hackthissite.org
  - data.hackthissite.org
  - speedtest2.hackthissite.org

- **External Redirects:**
  - hts.io (short domain)
