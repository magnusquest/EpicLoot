# DNS Recon
### Linux Commands

```bash
export TARGET="www.facebook.com"
whois $TARGET
nslookup $TARGET
dig $TARGET
```

### TheHarvester
 TheHarvester can be leveraged using the following scripts:

>Create a sources.txt file to automate TheHarvester

```bash
echo "baidu
bufferoverun
crtsh
hackertarget
otx
projecdiscovery
rapiddns
sublist3r
threatcrowd
trello
urlscan
vhost
virustotal
zoomeye" >> sources.txt
```

>Set target and pipe into TheHarvester, outputting files

```bash
export TARGET="facebook.com"
cat sources.txt | while read source; do theHarvester -d "${TARGET}" -b $source -f "${source}_${TARGET}";done
```

>Format and merge the output files

```bash
cat *.json | jq -r '.hosts[]' 2>/dev/null | cut -d':' -f 1 | sort -u > "${TARGET}_theHarvester.txt"
cat facebook.com_*.txt | sort -u > facebook.com_subdomains_passive.txt
```

## Tech Stalk Enumeration
```bash
export TARGET="www.facebook.com"
curl -I http://${TARGET}
whatweb -a 4 https://${TARGET} -v
```

[Wappalyzer](https://www.wappalyzer.com/) is a great plugin for web browser to enumerate tech stack.
 
 [WafW00f](https://github.com/EnableSecurity/wafw00f)  is a web application firewall (`WAF`) fingerprinting tool that sends requests and analyses responses to determine if a security solution is in place.

```bash
sudo apt install wafw00f -y
wafw00f -v https://www.tesla.com
```