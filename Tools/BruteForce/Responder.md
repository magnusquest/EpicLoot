# Responder
Responder is a LLMNR, NBT-NS and MDNS poisoner, with built-in HTTP/SMB/MSSQL/FTP/LDAP rogue authentication server supporting NTLMv1/NTLMv2/LMv2, Extended Security NTLMSSP and Basic HTTP authentication.

---

## Basic usage
Check if the interface is working with this and `ifconfig`

Launch Responder 
```shell
sudo responder -I {network_interface}
```
