# BurpSuite
Web interceptor multi-tool with automated attack scripts. Can intercept requests and responses.

---

### Basic Setup
1. Open `burpsuite`
2. Set Foxy Proxy to 127.0.0.1:8080
3. Go to Proxy -> Intercept tab
4. Check "Intercept is on" 

| Module   | Description                                                                            |
| -------- | -------------------------------------------------------------------------------------- |
| Proxy    | Can be used to intercept requests and alter them before being sent                     |
| Intruder | Allows the intercepted request to be programmatically mutated for attack with `ctrl+i` |
| Repeater | Re-send intercepted requests with `ctrl+r`, or `ctrl+shift+r`                          |
| Decoder  | Encode or Decode HTML, Unicode, Base64, or ASCII hex                                   |
|          |                                                                                        |


### Automatic Request/Response Modification
Go to (`Proxy>Options>Match and Replace`) and click on `Add` in Burp.

### Proxychains
To use `proxychains`, we first have to edit `/etc/proxychains.conf`, comment the final line and add the following two lines at the end of it:

```bash
#socks4         127.0.0.1 9050
http 127.0.0.1 8080
https 127.0.0.1 8080
```

We should also enable `Quiet Mode` to reduce noise by un-commenting `quiet_mode`. Once that's done, we can prepend `proxychains` to any command, and the traffic of that command should be routed through `proxychains` (i.e., our web proxy). For example, let's try using `cURL` on one of our previous exercises:

```bash
proxychains curl http://SERVER_IP:PORT
```