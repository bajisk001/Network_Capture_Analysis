# Wireshark Network Packet Capture Analysis

## 📌 Repository Overview
This repository contains live network packet captures and analysis using **Wireshark**. The objective is to **capture, filter, and analyze traffic for common protocols** including DNS, HTTP, TCP, UDP, ICMP, and TLS.

Each protocol has its dedicated folder containing:

- **Packet capture file (.pcap)**  
- **Analysis report (.md)** summarizing packet fields, communication flow, and observations.

---

## 🎯 Objective
- Capture live network packets and identify basic protocols and traffic types.
- Analyze the behavior and structure of network communication.
- Generate protocol-specific reports to understand packet details.

---

## 🛠 Tools Used
- **Wireshark** (Free, GUI-based packet capture tool)  
- Terminal commands (ping, curl) or web browsing to generate traffic.

---

## 📂 Folder Structure
DNS_Captures
├── DNS.pcapng
└── dns analysis.md

HTTP_Captures
├── HTTP.pcapng
└── http analysis.md

ICMP_Captures
├── ICMP.pcapng
└── icmp analysis.md

TCP_Captures
├── TCP.pcapng
└── tcp analysis.md

TLS_Captures
├── TLS.pcapng
└── tls analysis.md

UDP_Captures
├── UDP.pcapng
└── udp analysis.md
Wireshark_QA.md
README.md


---

## 🧭 Capture and Analysis Steps

1. **Install Wireshark** on your system.  
2. **Start packet capture** on your active network interface (Wi-Fi or Ethernet).  
3. **Generate traffic**:
   - Browse websites (HTTP/HTTPS/TLS)  
   - Ping servers (ICMP)  
   - Use commands like `curl`, `dig`, or streaming applications  
4. **Stop the capture** after ~30–60 seconds.  
5. **Filter packets** using Wireshark display filters:
   - `dns` → show only DNS packets  
   - `http` → show only HTTP packets  
   - `tcp` → show TCP packets  
   - `udp` → show UDP packets  
   - `icmp` → show ICMP packets  
   - `tls` → show TLS traffic  
6. **Identify at least 3 different protocols** in a single capture session.  
7. **Export the capture** as a `.pcap` or `.pcapng` file.  
8. **Summarize findings** for each protocol:
   - Packet fields  
   - Communication flow  
   - Observations (e.g., packet loss, handshake, encryption)

---

## ✅ Outcome
By completing this task, you will:

- Learn to **capture live network traffic** using Wireshark.  
- Understand **connectionless (UDP/ICMP) vs connection-oriented (TCP/TLS) protocols**.  
- Identify protocol-specific fields and behaviors.  
- Recognize **application-layer protocols** (DNS, HTTP, TLS) over network-layer protocols (TCP, UDP, ICMP).  

---

## 📎 Protocol-Specific Folders & Reports
- **DNS_Captures:** DNS query/response packets  
- **HTTP_Captures:** HTTP request/response packets  
- **ICMP_Captures:** Ping/Echo Request-Reply packets  
- **TCP_Captures:** TCP handshake, data transfer, and teardown  
- **TLS_Captures:** TLS handshake and encrypted application data  
- **UDP_Captures:** General UDP traffic  

Each folder contains:  
1. A `.pcap`/`.pcapng` file with the captured packets  
2. A Markdown report detailing the packet structure and analysis  

---

## 💡 Quick Tips
- Use **Display Filters** to isolate protocol-specific packets.  
- **Right-click → Follow → TCP/UDP/TLS Stream** to see complete conversations.  
- Analyze **packet length, flags, sequence numbers, and headers** to understand communication.  
- Remember: TLS and HTTPS traffic are encrypted; only handshake metadata is visible.  

---

## ⚡ Notes
- Multiple protocols can appear in the same capture (DNS, TCP, HTTP, ICMP).  
- Captures help understand both **network-layer and application-layer communication**.  
- Always save and document your captures for reporting and future analysis.

