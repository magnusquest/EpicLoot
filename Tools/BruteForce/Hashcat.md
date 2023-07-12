Brute force offline password cracking tool
[Example Hashes](https://hashcat.net/wiki/doku.php?id=example_hashes)
[Extra Tools](https://github.com/ZerBea/hcxtools)
https://github.com/hashcat/hashcat-utils.git
---
### Hashid
Used to identify hash type, usually ocurring as `$id$salt$hash` or `hash:salt`
```bash
pip install hashid
```
 The `-m` flag will attempt to determine the hashtype for hashcat

---
### Attack Modes

`-a` specifies attack mode

| Number | Mode            |
| ------ | --------------- |
| 0      | Straight        |
| 1      | Combination     |
| 3      | Brute-force     |
| 6      | Wordlist + Mask |
| 7      | Mask + Wordlist |

`-m` corresponds to the hash type

---
### Usage
Basic syntax:
```bash
hashcat -a 0 -m <hash type> <hash file> <wordlist>
```

Combination mode `1` uses two or more wordlists to combine them into an NxN wordlist
```bash
hashcat -a 1 -m <hash type> <hash file> <wordlist1> <wordlist2>
```

### Mask
Reduces keyspace while bruteforcing passwords

```bash
hashcat -a 3 -m 0 md5_mask_example_hash -1 01 'ILFREIGHT?l?l?l?l?l20?1?d'
```

![[Pasted image 20220829042725.png]]

---
### Hybrid
Used to generate wordlists from wordlists + mask. 6 will append, 7 will prepend.

```shell
hashcat -a 6 -m 0 hybrid_hash /opt/useful/SecLists/Passwords/Leaked-Databases/rockyou.txt '?d?s'
```

This command appends `0-9` and a special character to every entry in rockyou.txt

[[CUPP]] and CeWL are common tools for creating wordlists
[Keyboard Walks](https://github.com/hashcat/kwprocessor) are also common

---
### Rules
Rule files in `/usr/share/hashcat/rules/` can be used for more complex masks with the `-r` flag
>c so0 si1 se3 ss5 sa@ $2 $0 $1 $9

This example uses `c` to capitalize the first letter, `s` to substitute 'o' for '0' and '$d' to append


---
### Cracking WiFi MIC & PMKID
Use hcxpcapngtool  to format and extract hash

Cracking MIC uses mode 22000
