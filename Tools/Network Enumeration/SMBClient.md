Windows port 445 commonly hosts file shares that can be accessed with this tool

---

### Connect to Port 445
```bash
smbclient -N -L \\\\10.10.10.27\\foldername
```

`-N` Suppressed password prompt (anonymous login)
`-L` Allows you to look at what services are available on a server.