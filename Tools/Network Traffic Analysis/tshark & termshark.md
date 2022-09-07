# tshark
Command-line version of Wireshark for packet sniffing

---

## Basic Switches

| Switch Command | Result                                                                                                           |
| -------------- | ---------------------------------------------------------------------------------------------------------------- |
| -D             | Will display any interface available to capture from and then exit out.                                          |
| -L             | Will list the link-layer mediums you can capture from and then exit out.                                         |
| -i             | Choose an interface to capture from `-i eth0`                                                                    |
| -f             | Packet filter in libpcap syntax. used during capture                                                             |
| -c             | Grab a specific number of packets, then quit the program                                                         |
| -a             | Defines an autostop condition. Can be after a duration, specific file size, or after a certain number of packets |
| -r             | Read from a file                                                                                                 |
| -W             | Write to a file in pcap format                                                                                   |
| -P             | Will print the packet summary while writing into a file                                                          |
| -x             | Will addd Hex and ASCII output into the capture                                                                  |
| -h             | See the help menu                                                                                                                 |

---
# termshark
Text-based User Interface (TUI) application that provides a Wireshark-like interface in the terminal window
