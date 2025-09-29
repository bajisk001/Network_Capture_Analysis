# DNS Capture Analysis
## 1. Overview of DNS

- DNS (Domain Name System) is like the phonebook of the internet.
- When you type a website name like tryhackme.com in your browser, your computer doesn’t understand names — it needs an IP address (like 104.26.2.109) to connect.
- DNS translates the human-friendly name into the machine-friendly IP address.
- Without DNS, we’d have to remember long numbers instead of website names.

## How DNS works (simplified):
- You type a domain (tryhackme.com) into the browser.
- Your computer sends a DNS query to a DNS server.
- The server replies with the IP address of that domain.
- Your browser then connects to the website using that IP.

## 🎯 Objective
- Capture live network packets and identify basic protocols and traffic types.

- **Task:** Generate DNS traffic and analyze it with Wireshark.  
- **Focus:** Observe how a DNS query (domain name → IP address) works.  

## 🛠 Tools Used
- **Wireshark** (free, GUI-based packet capture tool).  
- **ping / browser** for generating network traffic.  

---

## 📂 Deliverables
1. A **packet capture file (.pcap)** containing DNS traffic.  
2. A **short report** summarizing identified protocols and packet details.  

---

## 🧭 Steps to Capture Packets

### 1. Traffic Generation
- Command used to generate DNS query Ex:ping picoctf.org/kalilinux etc


### 2. Packet Capture Details

- Tool used: Wireshark.

- Display filter (for analysis): dns
- Typical capture will show:
- **DNS Query** (Client → Server)  
- **DNS Response** (Server → Client)  
- Usually, 2–4 packets are generated per query.  

---

## 3. Wireshark Packet Fields (Explained Simply)

| Field           | What it Means in Layman Terms |
|-----------------|--------------------------------|
| **Transaction ID** | A unique number linking query ↔ response (like a token number). |
| **Flags**          | Indicates if it’s a query/response, recursion request, etc. |
| **Questions**      | Number of questions asked (e.g., “What is the IP of picoctf.org?”). |
| **Answer RRs**     | Number of answers (IP addresses in the reply). |
| **Queries**        | Domain name requested. |
| **Answers**        | IP addresses returned by the DNS server. |

---

## 4. Protocol Recognition
In Wireshark, DNS packets are easy to identify:
- **Protocol column:** shows `DNS`.  
- **Info column:**  
- `Standard query` → request.  
- `Standard query response` → reply.  
- **Port numbers:** UDP 53 (sometimes TCP 53 if data >512 bytes).  

---

## 5. Communication Flow
DNS over UDP is **connectionless** (no handshake like TCP).  

**Flow:**  
1. Client sends query: *“What is the IP of picoctf.org?”*  
2. DNS server replies: *“The IP is 34.207.192.240”* (example).  

👉 Both packets share the same **Transaction ID**.  

---

## 6. Observations / Notes
- DNS is fast: one query, one response.  
- If DNS response >512 bytes, TCP (port 53) is used.  
- Captured traffic helps identify:  
- The domain queried.  
- The resolved IP address.  
- Whether resolution was successful.  

---

## ✅ Outcome
- Learned how to capture packets with Wireshark.  
- Understood the role of DNS in translating domain names to IPs.  
- Identified multiple network protocols (DNS, HTTP/HTTPS, TCP/ICMP).  

---

## 📎 File Included
- `dns_capture.pcap` — contains DNS query/response packets for `picoctf.org`.  

