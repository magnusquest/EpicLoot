# Netstat
Command-line network utility that displays network connections for Transmission Control Protocol, routing tables, and a number of network interface and network protocol.

---

## Basic Usage
To check system processes on a port (ex: 80)
```bash
netstat -ltnp | grep -w '.:80'
```

-   `l` – tells netstat to only show listening sockets.
-   `t` – tells it to display tcp connections.
-   `n` – instructs it to show numerical addresses.
-   `p` – enables showing of the process ID and the process name.