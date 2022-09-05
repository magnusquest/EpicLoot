# SMBClient
Windows port 445 commonly hosts fileshares that can be accessed with this tool

---

### Connect to Port 445
```bash
smbclient -N -L \\\\10.10.10.27\\foldername
```