# Wireshark
Network Traffic Analysis tool with GUI

---

## Basics
To start a capture, click `Capture` in the toolbar and select the network interface

### Capture Filters
These are applied as capture is in progress and affects .pcap file when saved

| Filter          | Result                                                                                                   |
| --------------- | -------------------------------------------------------------------------------------------------------- |
| host            | `host` will filter visible traffic to show anything involving the designated host. Bi-directional        |
| src / dest      | `src` and `dest` are modifiers. We can use them to designate a source or destination host or port.       |
| net  x.x.x.x/24 | `net` will show us any traffic sourcing from or destined to the network designated. It uses / notation.  |
| proto           | will filter for a specific protocol type. (ether, TCP, UDP, and ICMP as examples)                        |
| port            | `port` is bi-directional. It will show any traffic with the specified port as the source or destination. |
| portrange       | `portrange` allows us to specify a range of ports. (0-1024)                                              |
| < / >           | `less` and `greater` can be used to look for a packet or protocol option of a specific size.             |
| and / &&        | `and` `&&` can be used to concatenate two different filters together. for example, src host AND port.    |
| or              | `or` allows for a match on either of two conditions. It does not have to meet both. It can be tricky.    |
| not             | `not` is a modifier saying anything but x. For example, not UDP.                                         |

### Display Filters
These are only applied to view and analyze results from a capture or .pcap file

| Display Filter             | Result                                            |
| -------------------------- | ------------------------------------------------- |
| ip.addr == x.x.x.x         | Capture only traffic pertaining to a certain host |
| ip.addr == x.x.x.x/24      | Capture traffic pertaining to a specific network  |
| ip.src / dst == x.x.x.x    | Capture traffic to or from a specific host        |
| dns / tcp / ftp / arp / ip | Filter traffic by a specific protocol             |
| tcp.port == x              | Filter by a specific tcp port                     |
| src.port / dst.port == x   | Specified port                                    |
| and / or / not             | Logical operators                                 |

### Folllowing TCP Streams
Wireshark can stitch TCP packets back together to recreate the entire stream in a readable format. This ability also allows us to pull data (`images, files, etc.`) out of the capture. This works for almost any protocol that utilizes TCP as a transport mechanism.

To utilize this feature:

-   right-click on a packet from the stream we wish to recreate.
-   select follow → TCP
-   this will open a new window with the stream stitched back together. From here, we can see the entire conversation.

### Extracting Data and Files From a Capture
Wireshark can recover many different types of data from streams. It requires you to have captured the entire conversation. 

To extract files from a stream:

-   stop your capture.
-   Select the File radial → Export → , then select the protocol format to extract from.
-   (DICOM, HTTP, SMB, etc.)

The basic steps to dissect FTP data from a pcap are as follows:
1.  Identify any FTP traffic using the `ftp` display filter.
2.  Look at the command controls sent between the server and hosts to determine if anything was transferred and who did so with the `ftp.request.command` filter.
3.  Choose a file, then filter for `ftp-data`. Select a packet that corresponds with our file of interest and follow the TCP stream that correlates to it.
4.  Once done, Change "`Show and save data as`" to "`Raw`" and save the content as the original file name.
5.  Validate the extraction by checking the file type.

---

## TLS Decryption
If you have the RSA key for encryption, it can be decrypted by Wireshark:
1. Go to Edit → Preferences → Protocols → TLS
2. On the TLS page, select Edit by RSA keys list → a new window will open.
3. Click the + to add a new entry
4. Enter the IP, Port, Protocol as `tpkt`, and the .key file

TLS data should now show in cleartext!


