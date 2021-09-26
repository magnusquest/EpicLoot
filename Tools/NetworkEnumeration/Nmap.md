# Nmap

Recon tool to enumerate open ports on an IP

---

### Basic Commands

This one is good for initial recon
```bash
nmap -sV 10.10.10.27
```

`-sC` provides some more information on specific ports like what version of SQL or SMB is being used

`-p-` will scan all ports past 1000 but will take longer
