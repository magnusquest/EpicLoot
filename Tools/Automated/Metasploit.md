Framework for automated vulnerability exploitation leveraging open source database

---

Start the console:
```shell
sudo msfconsole
```

Search for exploit
```shell
msf6 > search samba
```

Select exploit
```shell
msf6 > use 8
```

| Command or Option  | Description                  |
| ------------------ | ---------------------------- |
| `options`          | View available option        |
| `set OPTION VALUE` | Sets payload option to value |
| `run`              | Runs exploit with payload    |
| `RHOST`            | Remote target IP             |
| `RPORT`            | Remote target port           |
| `LHOST`            | Listener IP                  |
| `LPORT`            | Listener port                |

