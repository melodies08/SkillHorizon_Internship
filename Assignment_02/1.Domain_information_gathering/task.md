# Task 1: Domain Information Gathering

## Target
`hackthissite.org`

## Tools Used
- `whois`
- `dig` 
- `nslookup`

## Commands
```bash
whois hackthissite.org >> whois_hackthissite.txt
dig @192.168.174.2 hackthissite.org -t ANY >> dig_hackthissite.txt
nslookup hackthissite.org >> nslookup_hackthissite.txt
```

## Key Findings

### Domain Info
- **Created**: 2003-08-10 (~22 years old)
- **Registrar**: Porkbun LLC
- **Country**: US

### IP Addresses
- 137.74.187.100-104 (5 IPs for load balancing)

### DNS Servers
- c.ns.buddyns.com
- f.ns.buddyns.com  
- g.ns.buddyns.com
- h.ns.buddyns.com
- j.ns.buddyns.com

## Attack Surface
- Multiple IP addresses to test
- External DNS provider (BuddyNS)
- Admin email: admin@hackthissite.org
