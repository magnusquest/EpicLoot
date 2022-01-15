# Nmap

Network Mapper (`Nmap`) is an open-source network analysis and security auditing tool written in C, C++, Python, and Lua. It is designed to scan networks and identify which hosts are available on the network using raw packets, and services and applications, including the name and version, where possible. It can also identify the operating systems and versions of these hosts. Besides other features, Nmap also offers scanning capabilities that can determine if packet filters, firewalls, or intrusion detection systems (IDS) are configured as needed.

By default, `Nmap` scans the top 1000 TCP ports with the SYN scan (`-sS`). This SYN scan is set only to default when we run it as root because of the socket permissions required to create raw TCP packets. Otherwise, the TCP scan (`-sT`) is performed by default.

---

## Basic Commands

This one is good for initial recon
```bash
nmap -sV 10.10.10.27
```


### Options

| <div style="width:140px">**Flag**</div> | **Description**                                                                                    |
| ----------------------------------- | ---------------------------------------------------------------------------------------------- |
| `-sV`                               | Service Version info                                                                           |
| `-sC`                               | provides some more information on specific ports like what version of SQL or SMB is being used |
| `-p-`                               | will scan all ports past 1000 but will take longer                                             |
| `-oN`                               | normal output to file                                                                          |
| `-iL`                               | to input file list of hosts                                                                    |
| `--reason`                          | Gives reason for determining port status                                                       |
| `--packet-trace`                    | shows sent and recieved packets during scan process                                            |
| `-A`                                | aggressive scan which includes `-O -sV -sC --traceroute`                                       |
| `-O`                                | OS detection                                                                                   |
| `-PE`                               | use ICMP echo request instead of default ARP request                                           |
| `-Pn`                               | disable ICMP echo requests                                                                     |
| `-n`                                | disable DNS resolution                                                                         |
| `--disable-arp-ping`                | disable ARP. When used with `-Pn` will send TCP-SYN packets                                    |
| `-F`                                | Target top 100 ports                                                                           |
| `-sU`                               | Use UDP scan                                                                                   |


---

## Scripts

Nmap has the ability to perform scripted functions via Nmap Scripting Engine (NSE) in Lua. These are the default scripts which can be accessed using one of the following commands:
```
--script <category>
--script <script-name>,<script-name>
```

| **Category** | **Description**                                                                                                                         |
| ------------ | --------------------------------------------------------------------------------------------------------------------------------------- |
| `auth`       | Determination of authentication credentials.                                                                                            |
| `broadcast`  | Scripts, which are used for host discovery by broadcasting and the discovered hosts, can be automatically added to the remaining scans. |
| `brute`      | Executes scripts that try to log in to the respective service by brute-forcing with credentials.                                        |
| `default`    | Default scripts executed by using the `-sC` option.                                                                                     |
| `discovery`  | Evaluation of accessible services.                                                                                                      |
| `dos`        | These scripts are used to check services for denial of service vulnerabilities and are used less as it harms the services.              |
| `exploit`    | This category of scripts tries to exploit known vulnerabilities for the scanned port.                                                   |
| `external`   | Scripts that use external services for further processing.                                                                              |
| `fuzzer`     | This uses scripts to identify vulnerabilities and unexpected packet handling by sending different fields, which can take much time.     |
| `intrusive`  | Intrusive scripts that could negatively affect the target system.                                                                       |
| `malware`    | Checks if some malware infects the target system.                                                                                       |
| `safe`       | Defensive scripts that do not perform intrusive and destructive access.                                                                 |
| `version`    | Extension for service detection.                                                                                                        |
| `vuln`       | Identification of specific vulnerabilities.                                                                                             | 

### Useful Scripts


| **Script** | **Description**                                          |
| ---------- | -------------------------------------------------------- |
| `banner`   | Displays the banner recieved from connecting to the port |


## Firewalls & IDS/IPS
Dealing with firewallas and intruder detection/prevention systems can be tricky. Here are some stealthy options:

| <div style="width:140px">**Flag**</div> | **Description**                                                                                                                      |
| --------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| `-sA`                                   | TCP ACK scan; only sends a TCP packet with the `ACK` flag.                                                                           |
| `-sS`                                   | TCP SYN scan                                                                                                                         |
| `-sT`                                   | TCP connect scan                                                                                                                     |
| `-D RND:5`                              | Send packets with 5 random fake IPs                                                                                                  |
| `-S <IP_Address>`                       | Spoof source address                                                                                                                 |
| `-e <iface>`                            | Use specified interface such as 'eth0' or 'tun0'                                                                                     |
| `--dns-server <ns>, <ns>`               | Specify DNS server for DNS resolution, in some cases a private DNS can be more trusted and therefore bypass IDS/IPS and firewalls    |
| `--source-port 53`                      | DNS queries are made over `UDP port 53`; `TCP port 53` is now being used more frequently and may be able to bypass security measures |
| `--top-ports <#>`                       | Scan the top <#> ports. Useful to remain undetected                                                                                  |


### Proxies
To intercept requests/responses with [[BurpSuite]]:
```bash
nmap --proxies http://127.0.0.1:8080 SERVER_IP -pPORT -Pn -sC
```

---

### Notes
To find target OS, run this command:
```bash
sudo nmap <target> -p 22 --source-port 53 --script banner
```

To find DNS server information use this command:
```bash
sudo nmap <target> -sSU -p 53 --script dns-nsid
```

---