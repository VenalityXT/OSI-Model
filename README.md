# OSI Model – Practical Networking and Security Reference

The OSI (Open Systems Interconnection) Model is used to understand how data moves through a network by separating responsibilities into layers. Each layer builds on the one below it, adding structure and meaning until raw signals become usable applications.

In real environments, the OSI model is most useful as a **troubleshooting and security analysis framework**. Network engineers, SOC analysts, and security engineers rely on it to quickly narrow down where a problem or attack exists.

---

<p align="center">
 <img src=https://github.com/user-attachments/assets/fff92046-580e-4130-82fc-3fc928c4cfbf>
</p>

---

The Physical Layer covers the actual transmission of bits across physical media. It defines how data is moved electrically, optically, or wirelessly and provides the foundation that all higher layers rely on. This layer has no awareness of addresses, protocols, or applications.

<img width="594" height="192" alt="image" src="https://github.com/user-attachments/assets/987f3a54-a121-4279-8a56-5e7d14800ab4" />

If the physical layer is not functioning, nothing above it can operate.

**Major Things to Know**
- Cables, fiber, wireless signals
- NICs, ports, link lights
- Signal strength and interference

**Real-World Examples**
- pfSense or OPNsense interfaces showing link up/down status
- Network switch port LEDs
- Wireshark showing no packets at all due to no signal

**Common Problems | Simple Checks**

Cable unplugged or damaged | Reseat or replace cable  
No link light | Verify NIC, port, and power  
Wrong media type | Confirm copper vs fiber compatibility  
Wireless interference | Change channel or reposition AP  

---

<p align="center">
 <img src=https://github.com/user-attachments/assets/e66da7c3-d7e2-4524-b81a-aa45fbaacc5f>
</p>

---

The Data Link Layer enables communication between devices on the same local network. It builds on the physical signal by organizing data into frames and using MAC addresses to identify devices. Switches operate at this layer, forwarding traffic within a network segment.

<img width="594" height="239" alt="image" src="https://github.com/user-attachments/assets/4bfb0fd0-8685-4a6f-81aa-aaf9afb72b56" />

This layer is responsible for **local delivery before routing exists**.

**Major Things to Know**
- MAC addresses (physical identifiers)
- Ethernet frames
- ARP (IP to MAC resolution)
- VLAN segmentation

**Real-World Examples**
- pfSense or OPNsense ARP table
- Managed switch VLAN configuration
- Wireshark capturing ARP requests and replies

**Common Problems | Simple Checks**

ARP not resolving | Clear ARP cache and verify IP mapping  
Wrong VLAN | Check switch port VLAN assignment  
Duplicate MAC | Inspect cloned VMs or misconfigured NICs  
Connected but no traffic | Verify switch forwarding and VLANs  

---

<p align="center">
 <img src=https://github.com/user-attachments/assets/d974a40a-f67c-4d6e-97bd-d697e5ea30d2>
</p>

---

The Network Layer introduces logical addressing and routing, allowing traffic to move between networks. It builds on Layer 2 by deciding where traffic should be forwarded once it leaves the local segment.

<img width="594" height="239" alt="image" src="https://github.com/user-attachments/assets/20dadd65-715e-49f2-a39a-e4538218fbdd" />

This layer answers how packets move from one network to another.

**Major Things to Know**
- IP addresses and subnetting
- Routing tables
- ICMP for diagnostics

**IPv4 vs IPv6**
- IPv4 uses 32-bit addresses and commonly relies on NAT
- IPv6 uses 128-bit addresses and provides globally unique addressing

**Real-World Examples**
- pfSense or OPNsense routing table
- Firewall gateway configuration
- Wireshark capturing ICMP echo requests and replies

**Common Problems | Simple Checks**

Incorrect IP | Verify IP, subnet mask, and gateway  
Cannot reach other networks | Check routing table and default route  
Ping fails | Ensure ICMP is allowed  
IP conflict | Check DHCP leases and static assignments  

---

<p align="center">
 <img src=https://github.com/user-attachments/assets/b8a52156-ad59-44c1-99f6-3da8f7d2648f>
</p>

---

The Transport Layer manages end-to-end communication between systems. It builds on routing by ensuring data reaches the correct service on the destination host using ports and connection logic.

<img width="594" height="239" alt="image" src="https://github.com/user-attachments/assets/812a0ac9-b481-43cc-9fa3-69cfbf2ae414" />

This layer determines reliability and flow control.

**Major Things to Know**
- Ports
- TCP vs UDP
- Connection states

**TCP vs UDP**
- TCP is reliable, ordered, and connection-based
- UDP is faster, connectionless, and does not guarantee delivery

**Real-World Examples**
- pfSense or OPNsense firewall rules allowing or blocking ports
- Wireshark capturing TCP handshakes
- IDS alerts for port scans or SYN floods

**Common Problems | Simple Checks**

Service unreachable | Confirm correct port is open  
Connection timeout | Check firewall rules and TCP state  
Intermittent issues | Inspect retransmissions and packet loss  
Port scan detected | Review firewall and IDS logs  

---

<p align="center">
 <img src=https://github.com/user-attachments/assets/79e2b824-ccbc-4662-bc3a-d304b7e0173b>
</p>

---

The Session Layer manages session establishment, persistence, and teardown. It builds on the transport layer by maintaining continuity across multiple exchanges instead of treating each packet independently.

<img width="358" height="239" alt="image" src="https://github.com/user-attachments/assets/df9ed790-b99c-4337-8e7e-c06ed51539d3" />

Issues at this layer often appear inconsistent rather than fully broken.

**Major Things to Know**
- Session tracking
- Authentication persistence
- Timeouts and keepalives

**Real-World Examples**
- pfSense or OPNsense state tables
- VPN session management
- Wireshark tracking long-lived connections

**Common Problems | Simple Checks**

Session drops | Review timeout and keepalive settings  
Repeated logins | Check session persistence  
Random disconnects | Inspect state table behavior  
Session reuse | Validate authentication tokens  

---

<p align="center">
 <img src=https://github.com/user-attachments/assets/b3e67a86-22ff-452e-9737-6b6b0e882848>
</p>

---

The Presentation Layer ensures data is formatted, encoded, and encrypted correctly. It builds on sessions by transforming data into a secure and usable format before it reaches the application.

<img width="594" height="239" alt="image" src="https://github.com/user-attachments/assets/05c44300-6a59-42fd-ab6d-4b65a89f2554" />

Encryption and encoding failures commonly surface here.

**Major Things to Know**
- TLS and SSL
- Encryption and decryption
- Encoding formats

**Real-World Examples**
- HTTPS inspection in Wireshark
- pfSense certificate management
- TLS handshake errors in browser logs

**Common Problems | Simple Checks**

Certificate error | Verify certificate chain and expiration  
TLS failure | Check supported protocols and ciphers  
Unreadable data | Confirm encoding compatibility  
Encryption mismatch | Align client and server settings  

---

<p align="center">
 <img src=https://github.com/user-attachments/assets/a8578348-ac38-47d1-8a60-2b1f8bd52661>
</p>

---

The Application Layer is where users and services interact with the network. It builds on all lower layers to provide usable functionality such as web access, email, file transfer, and APIs.

<img width="661" height="239" alt="image" src="https://github.com/user-attachments/assets/9e64f0c5-4cdf-4fff-b585-4f616fd979ae" />

Most visible issues occur here, even when the root cause exists below.

**Major Things to Know**
- Application protocols (HTTP, DNS, SMTP, FTP)
- Service logic
- User authentication

**Real-World Examples**
- Web servers behind pfSense or OPNsense
- DNS queries observed in Wireshark
- Application logs indicating backend failures

**Common Problems | Simple Checks**

Website not loading | Check DNS and service status  
Application error | Verify backend connectivity  
Login failure | Review authentication and session handling  
Slow performance | Inspect latency at lower layers  

---

Using the OSI model allows network and security professionals to troubleshoot logically, communicate clearly, and defend systems effectively. Each layer narrows the problem space until the true cause is identified.
