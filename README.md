<h1 align="center">OSI Model – Practical Networking and Security Reference</h1>

The OSI (Open Systems Interconnection) Model is used to understand how data moves through a network by separating responsibilities into layers. Each layer builds on the one below it, adding structure and meaning until raw signals become usable applications.

In real environments, the OSI model is most useful as a **troubleshooting and security analysis framework**. Network engineers, SOC analysts, and security engineers rely on it to narrow down where a problem or attack exists instead of troubleshooting blindly.

---

<p align="center">
 <img src=https://github.com/user-attachments/assets/fff92046-580e-4130-82fc-3fc928c4cfbf>
</p>

---

The Physical Layer handles the transmission of raw bits across a physical medium. It defines how data is moved electrically, optically, or wirelessly and provides the foundation that all higher layers rely on. At this stage, data has no structure or meaning.

<img width="594" height="192" alt="image" src="https://github.com/user-attachments/assets/987f3a54-a121-4279-8a56-5e7d14800ab4" />

If this layer fails, communication stops entirely, regardless of how correct the configuration is above it.

**Key Things to Know**
- Deals with signals, not data
- Uses physical media (copper, fiber, wireless)
- Involves NICs, ports, link lights, and signal strength

Packet capture tools will show no traffic at all if the signal never reaches the interface, which is why physical checks always come first during troubleshooting.

**Common Problems | Simple Checks**

Cable unplugged or damaged -> Reseat or replace the cable  
No link light          -> Verify NIC, switch port, and power  
Incorrect media type   -> Confirm copper vs fiber compatibility  
Wireless interference  -> Change channel or reposition access point  

---

<p align="center">
 <img src=https://github.com/user-attachments/assets/e66da7c3-d7e2-4524-b81a-aa45fbaacc5f>
</p>

---

The Data Link Layer enables communication between devices on the same local network. It builds on the physical signal by framing data and using hardware identifiers so devices know where to send traffic locally.

<img width="594" height="239" alt="image" src="https://github.com/user-attachments/assets/4bfb0fd0-8685-4a6f-81aa-aaf9afb72b56" />

This layer allows higher layers to function without knowing anything about cables or voltages.

**Key Things to Know**
- Uses MAC addresses
- Responsible for Ethernet frames
- Handles ARP resolution
- Supports VLAN segmentation

Switches operate here, forwarding frames based on MAC addresses. When ARP fails, devices may know *where* to send traffic logically but not *how* to reach it physically.

**Common Problems | Simple Checks**

ARP not resolving | Clear ARP cache and verify IP-to-MAC mapping  
Incorrect VLAN | Confirm switch port VLAN assignment  
Duplicate MAC address | Check cloned virtual machines  
Connected but no traffic | Verify switching and VLAN forwarding  

---

<p align="center">
 <img src=https://github.com/user-attachments/assets/d974a40a-f67c-4d6e-97bd-d697e5ea30d2>
</p>

---

The Network Layer introduces logical addressing and routing, allowing traffic to move between different networks. It builds on Layer 2 by deciding where packets should be forwarded once they leave the local segment.

<img width="594" height="239" alt="image" src="https://github.com/user-attachments/assets/20dadd65-715e-49f2-a39a-e4538218fbdd" />

This is the first layer where traffic is no longer limited to the local network.

**Key Things to Know**
- Uses IP addresses
- Handles routing decisions
- Supports subnetting and gateways
- Uses ICMP for diagnostics

IPv4 uses 32-bit addresses and commonly relies on NAT, while IPv6 uses 128-bit addresses and enables globally unique addressing. Routers and firewalls rely on routing tables at this layer to move traffic correctly.

**Common Problems | Simple Checks**

Incorrect IP configuration | Verify IP address, subnet mask, and gateway  
Cannot reach other networks | Check routing table and default route  
Ping fails | Confirm ICMP is permitted  
IP conflict | Review DHCP leases and static assignments  

---

<p align="center">
 <img src=https://github.com/user-attachments/assets/b8a52156-ad59-44c1-99f6-3da8f7d2648f>
</p>

---

The Transport Layer manages end-to-end communication between systems. It builds on routing by delivering data to the correct service on a host using ports and connection logic.

<img width="594" height="239" alt="image" src="https://github.com/user-attachments/assets/812a0ac9-b481-43cc-9fa3-69cfbf2ae414" />

This layer defines how reliable or fast communication should be.

**Key Things to Know**
- Uses port numbers
- Supports TCP and UDP
- Tracks connection state

TCP provides reliable, ordered delivery, while UDP prioritizes speed and low overhead. Firewalls commonly enforce policy at this layer by controlling which ports and protocols are allowed.

> [!NOTE]
> Although IP addressing belongs to Layer 3, Layer 4 still depends on IP addresses to establish end-to-end communication between hosts.

**Common Problems | Simple Checks**

Service unreachable | Verify the correct port is open  
Connection timeout | Inspect firewall rules and transport state  
Intermittent connectivity | Check retransmissions and packet loss  
Unexpected scans | Review firewall and intrusion alerts  

---

<p align="center">
 <img src=https://github.com/user-attachments/assets/79e2b824-ccbc-4662-bc3a-d304b7e0173b>
</p>

---

The Session Layer maintains continuity between communicating systems. It builds on the transport layer by tracking session state across multiple exchanges rather than treating each packet independently.

<img width="358" height="239" alt="image" src="https://github.com/user-attachments/assets/df9ed790-b99c-4337-8e7e-c06ed51539d3" />

Issues here often feel inconsistent and difficult to reproduce.

**Key Things to Know**
- Tracks session state
- Manages authentication persistence
- Controls timeouts and keepalives

State tables and session tracking mechanisms help maintain long-lived connections such as VPNs and authenticated services.

**Common Problems | Simple Checks**

Session drops | Review timeout and keepalive settings  
Repeated authentication | Check session persistence configuration  
Random disconnects | Inspect state tracking behavior  
Session reuse | Validate authentication token handling  

---

<p align="center">
 <img src=https://github.com/user-attachments/assets/b3e67a86-22ff-452e-9737-6b6b0e882848>
</p>

---

The Presentation Layer ensures data is formatted, encoded, and encrypted correctly before it reaches the application. It builds on sessions by transforming data into a secure and usable form.

<img width="594" height="239" alt="image" src="https://github.com/user-attachments/assets/05c44300-6a59-42fd-ab6d-4b65a89f2554" />

Failures here often appear as application issues even when the service itself is functioning.

**Key Things to Know**
- Handles encryption and decryption
- Manages encoding and compression
- Uses TLS and SSL

Encryption mismatches or certificate issues at this layer can prevent applications from functioning even though network connectivity is intact.

**Common Problems | Simple Checks**

Certificate error | Verify certificate chain and expiration  
TLS handshake failure | Check supported protocols and ciphers  
Unreadable data | Confirm encoding compatibility  
Encryption mismatch | Align client and server settings  

---

<p align="center">
 <img src=https://github.com/user-attachments/assets/a8578348-ac38-47d1-8a60-2b1f8bd52661>
</p>

---

The Application Layer is where users and services directly interact with the network. It builds on all lower layers to deliver usable functionality.

<img width="661" height="239" alt="image" src="https://github.com/user-attachments/assets/9e64f0c5-4cdf-4fff-b585-4f616fd979ae" />

Most visible failures occur here, but the root cause often exists lower in the stack.

**Key Things to Know**
- Uses application protocols (HTTP, DNS, SMTP, FTP)
- Handles user interaction and service logic
- Relies on all lower layers

Understanding the OSI model prevents misdiagnosing application errors that are actually caused by transport, routing, or encryption failures.

**Common Problems | Simple Checks**

Website not loading | Check DNS resolution and service status  
Application error | Verify backend connectivity  
Login failure | Review authentication and session handling  
Poor performance | Inspect latency and transport behavior  

---

## Summary

The OSI Model provides a structured way to understand how data moves through a network by separating complex communication processes into clearly defined layers. Rather than serving as a strict implementation guide, the model functions as a **mental framework** that allows networking and security professionals to reason about failures, attacks, and design decisions logically.

By mapping real-world tools, protocols, and behaviors to each layer, this project demonstrates how the OSI model is applied during troubleshooting and security analysis. Physical issues are isolated before logical ones, local communication is validated before routing, and application errors are examined in the context of transport, encryption, and session handling.

Understanding the OSI model in this way prevents misdiagnosis, reduces troubleshooting time, and improves communication between technical teams. When used correctly, it allows professionals to identify not just *what* is failing, but *where* and *why* the failure is occurring.

