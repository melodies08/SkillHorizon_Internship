# Task 3: Email & Employee Information

## Target
`hackthissite.org`

## Tools Used
- `theHarvester`

## Commands
```bash
theHarvester -d hackthissite.org -b bing,brave,duckduckgo,hunter,otx,yahoo | tee theHarvester_hackthissite.txt
```

## Key Findings

### Emails Found (1)
- sam@hackthissite.org

### IP Addresses Discovered (33)
**Main Infrastructure (137.74.187.x):**
- 137.74.187.100-104 (Primary web servers)
- 137.74.187.133-134 (Mirror services)
- 137.74.187.137 (Legal)
- 137.74.187.150-153 (IRC services)

**Development Servers (198.148.81.x):**
- 198.148.81.135-144 (Dev/staging range)

**External Services:**
- 185.199.108-111.153 (GitHub Pages)
- 185.24.222.13 (IRC Wolf server)
- 67.21.66.227-230 (External hosting)
- 89.106.200.1, 89.41.169.49 (Additional services)

### Hosts Confirmed (16)
- ctf.hackthissite.org
- data.hackthissite.org
- forum.hackthissite.org
- forums.hackthissite.org
- h5ai.hackthissite.org
- irc.hackthissite.org
- irc-v6.hackthissite.org
- legal.hackthissite.org
- lille.irc.hackthissite.org
- lille.irc-v6.hackthissite.org
- mirror.hackthissite.org
- qdb.hackthissite.org
- speedtest2.hackthissite.org
- status.hackthissite.org
- wolf.irc.hackthissite.org
- wolf.irc-v6.hackthissite.org
