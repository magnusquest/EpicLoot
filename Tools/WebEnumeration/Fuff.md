Fuff is a tool used for web fuzzing. Fuzzing is a technique used to test inputs in blackbox environments against wordlists. These wordlists, commonly under `/opt/useful/SecLists/Discovery/Web-Content`, contain possible matches to directories, passwords, usernames, etc.

___

## Basic Usage

Before using a wordlist, trim the fat:
```bash
sudo sed -i 's/^\#.*$//g' /opt/useful/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt && sudo sed -i '/^$/d' /opt/useful/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt
```

This command will fuzz for possible directories from the small wordlist:
```bash
ffuf -w /opt/useful/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ -u http://188.166.173.208:30708/FUZZ -c
```

Use the following command to fuzz for web-extensions to determine which can be used to fuzz further:
```bash
ffuf -w /opt/useful/SecLists/Discovery/Web-Content/web-extensions.txt:FUZZ -u http://188.166.173.208:31331/blog/indexFUZZ -c
```

Once the extension has been found (`.php` in this example), use this command:
```bash
ffuf -w /opt/useful/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ -u http://188.166.173.208:30708/blog/FUZZ.php -c
```

---
## Recursive Fuzzing
When we scan recursively, it automatically starts another scan under any newly identified directories that may have on their pages until it has fuzzed the main website and all of its subdirectories.

In `ffuf`, we can enable recursive scanning with the `-recursion` flag, and we can specify the depth with the `-recursion-depth` flag. If we specify `-recursion-depth 1`, it will only fuzz the main directories and their direct sub-directories.

If any sub-sub-directories are identified (like `/login/user`, it will not fuzz them for pages). 
When using recursion in `ffuf`, we can specify our extension with `-e .php`

```bash
ffuf -w /opt/useful/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ -u http://167.71.128.208:30129/FUZZ -recursion -recursion-depth 1 -e .php -v -c
```

Working with multiple wordlists:
```bash
ffuf -w ./folders.txt:FOLDERS,./wordlist.txt:WORDLIST,./extensions.txt:EXTENSIONS -u http://192.168.10.10/FOLDERS/WORDLISTEXTENSIONS
```


___
## DNS Subdomain Fuzzing
Use `/opt/useful/SecLists/Discovery/DNS/` to fuzz for subdomains such as `*.google.com*`

```bash
ffuf -w /opt/useful/SecLists/Discovery/DNS/subdomains-top1million-5000.txt:FUZZ -u https://FUZZ.hackthebox.eu/
```


## VHOST Fuzzing
VHosts may or may not have public DNS records. 
>Add a VHOST with the following command:
sudo sh -c 'echo "167.71.128.208  academy.htb" >> /etc/hosts'

We can fuzz them with the `-H 'Host: FUZZ.academy.htb'` parameter:

```bash
ffuf -w /opt/useful/SecLists/Discovery/DNS/subdomains-top1million-5000.txt:FUZZ -u http://academy.htb:PORT/ -H 'Host: FUZZ.academy.htb' -fs 900
```
The `-fs 900` flag is used to filter out HTTP response size of 900 Bytes since all responses come as 200 status codes, we want to find a page that is different based on the header.

___

## HTTP Parameter Fuzzing 
To enumerate a website with hidden queries or parameters:
```bash
ffuf -w /opt/useful/SecLists/Discovery/Web-Content/burp-parameter-names.txt:FUZZ -u http://admin.academy.htb:PORT/admin/admin.php?FUZZ=key -fs xxx
```

Using the `-d` flag to add a payload for a `-X POST`  request:
```bash
ffuf -w /opt/useful/SecLists/Discovery/Web-Content/burp-parameter-names.txt:FUZZ -u http://admin.academy.htb:PORT/admin/admin.php -X POST -d 'FUZZ=key' -H 'Content-Type: application/x-www-form-urlencoded' -fs xxx
```

>Tip: In PHP, "POST" data "content-type" can only accept "application/x-www-form-urlencoded". So, we can set that in "ffuf" with "-H 'Content-Type: application/x-www-form-urlencoded'".

To create a list of ID's for fuzzing: `for i in $(seq 1 1000); do echo $i >> ids.txt; done`

```bash
ffuf -w ids.txt:FUZZ -u http://admin.academy.htb:PORT/admin/admin.php -X POST -d 'id=FUZZ' -H 'Content-Type: application/x-www-form-urlencoded' -fs xxx
```

---

## Useful 
[[CeWL|Creating Wordlists with CeWL]]