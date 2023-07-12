Directory brute forcing tool for web

---

## Basic
```shell
gobuster dir --url http://10.129.203.32/ --wordlist /usr/share/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt 
```

```shell
gobuster vhost -w /opt/useful/SecLists/Discovery/DNS/subdomains-top1million-5000.txt -u http://thetoppers.htb
```

| Switch | Effect                                |
| ------ | ------------------------------------- |
| `-x`   | Scan for specific file type extension |
|        |                                       |
