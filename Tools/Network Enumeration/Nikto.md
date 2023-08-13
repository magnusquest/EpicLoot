Automated web scanner

To perform a simple domain scan, use the `-h` (host) flag:
```shell
nikto -h scanme.nmap.org
```

For domains with HTTPS enabled, you have to specify the `-ssl` flag to scan port 443:
```shell
nikto -h https://nmap.org -ssl
```

To export a scan result, use the `-o` flag followed by the file name:
```shell
nikto -h scanme.nmap.org -o scan.txt
```

Nikto offers a way to export scans to Metasploit so that it gets easier when you try to exploit systems based on the scan results from Nikto.

To do that, append the `-Format msf+` flag to the end of a scan:
```shell
nikto -h <domain/ip> -Format msf+
```

