# Capture-and-analysis

#  Wireshark Network Traffic Analysis 
This repository contains a comprehensive network traffic analysis conducted on Kali Linux using Wireshark.  
The purpose of this task is to understand packet-level communication on a network, observe different protocols in action, and gain hands-on familiarity with traffic inspection.

This experiment demonstrates live packet capture, filtering, interpretation, and exporting capture data for further analysis.



#  **Task Objectives**
1. Install or open Wireshark on Kali Linux.
2. Capture real-time network traffic.
3. Generate traffic using common tools (browser, ping).
4. Apply display filters to isolate specific protocols.
5. Identify at least three protocols.
6. Export the captured packets as a `.pcapng` file.
7. Provide a detailed summary of findings and observed packet behaviors.



#  **Environment Setup**
- **Operating System:** Kali Linux (VM environment)
- **Network Adapter:** `eth0` (NAT/Bridged — default for VMs)
- **Tool Used:** Wireshark
- **Additional Tools:**
  - `ping` command (ICMP traffic)
  - Firefox Browser (for DNS, TCP, TLS, QUIC)
  - Linux terminal



#  **Step-by-Step Procedure (Detailed)**
*1. Launching Wireshark**
Wireshark was opened from:
Upon launching, the available interfaces were:
- **eth0** (active interface)
- **lo** (loopback)
Since this Kali Linux instance is running in a VM, Wi-Fi interfaces like `wlan0` do not appear; instead, VM provides a NAT/Bridged Ethernet interface (`eth0`).

*2. Starting the Capture**
- Selected `eth0` as the capturing interface.
- Clicked the **blue shark fin** icon to begin packet capture.
- Wireshark began displaying real-time packets flowing through the VM network interface.

*3. Generating Network Traffic**
To produce various types of packets, two methods were used:

*4. Stopping the Capture
After generating traffic, the packet capture was stopped by clicking the red square (Stop) button in Wireshark.
Stopping the capture finalizes the collected data and allows the file to be saved and analyzed.

*5. Applying Display Filters
Wireshark provides powerful display filters that help isolate specific types of packets.
The following display filters were applied during analysis:
Protocol	Purpose	Filter Used
TCP	Reliable, connection-oriented communication	tcp
UDP	Fast, connectionless traffic (used by DNS and QUIC)	udp
TLS/SSL	Encrypted HTTPS communication	tls
DNS	Domain name resolution queries and responses	dns
ARP	Resolves local IP ↔ MAC addresses	arp
QUIC	Modern Google protocol running over UDP	quic
Each filter allowed me to view only the packets related to that specific protocol, making the analysis clearer and more detailed.




#  **Detailed Protocol Analysis
Below is an in-depth explanation of each protocol identified during the capture session. Each protocol plays a specific role in network communication and contributes to how devices interact on the internet.

 TCP (Transmission Control Protocol)
Purpose: Provides reliable, connection-oriented communication.
Observed Behavior:
SYN → SYN-ACK → ACK handshake during Google connection.
Carried encrypted TLS data after connection was established.
Use Case: HTTPS browsing, application communication.

 UDP (User Datagram Protocol)
Purpose: Fast, connectionless protocol with low overhead.
Observed Behavior:
Used for DNS queries.
Used by QUIC for faster encrypted browsing.
Use Case: Streaming, gaming, DNS, QUIC-based traffic.

 TLS (Transport Layer Security)
Purpose: Encrypts all HTTPS web traffic.
Observed Behavior:
TLS handshake packets (Client Hello, Server Hello).
Encrypted application data that cannot be read directly.
Use Case: Secure websites (HTTPS).

 DNS (Domain Name System)
Purpose: Converts domain names (google.com) to IP addresses.
Observed Behavior:
DNS query sent to resolve Google’s server IP.
DNS response showing public IPs like 142.x.x.x.
Use Case: Every website access begins with DNS.

 ARP (Address Resolution Protocol)
Purpose: Maps IP addresses to MAC addresses inside the local network.
Observed Behavior:
ARP requests: “Who has 10.x.x.x?”
ARP replies with corresponding MAC addresses.
Use Case: Local network communication.

 QUIC (Quick UDP Internet Connections)
Purpose: Modern encrypted protocol developed by Google, faster than TCP.
Observed Behavior:
QUIC packets over UDP on port 443.
Encrypted payload similar to TLS but more efficient.
Use Case: YouTube, Google Search, Chrome traffic.

 ICMP (Internet Control Message Protocol)**
Purpose: Used for diagnostic operations such as ping.  
Observed Behavior:
ICMP Echo Requests sent to Google.  
ICMP Echo Replies received.  
Use Case:** Connectivity testing.



 #  ** Findings and Observations

During the capture and analysis:

Over 215+ packets were collected in a short time.

Simple browsing activity (visiting Google) triggered multiple protocols working together.

ICMP confirmed active connectivity via ping.

DNS resolved domain names before establishing connections.

TCP established reliable connections for HTTPS.

TLS encrypted the actual web content.

QUIC provided faster encrypted transport for Google services.

ARP handled local IP-to-MAC mapping inside the VM environment.




##### NOTE:

All visible IPs were either:

Private IP (10.x.x.x): safe and internal

Public server IPs (Google, Cloudflare)

No sensitive or personal information was exposed in the capture.



#  ** Conclusion

This Wireshark capture and analysis task provided valuable hands-on experience with:

Monitoring live network traffic

Understanding how internet protocols work in practice

Analyzing encrypted and unencrypted packets

Identifying multiple protocol types

Using Wireshark filters effectively

The experiment successfully demonstrates how multiple networking layers and protocols collaborate when performing everyday actions such as browsing the web or sending ICMP requests.

