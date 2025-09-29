# TLS Capture Analysis

## 1. Overview of TLS

- **TLS (Transport Layer Security)** is a protocol that encrypts data between a client and server to ensure **privacy, integrity, and authenticity**.  
- TLS is widely used for secure web browsing (HTTPS), email, and other sensitive communications.  
- Think of TLS as an **envelope** for your message — even if someone intercepts it, they cannot read or tamper with the contents.  

**Common applications that use TLS:**  
- HTTPS (web browsing)  
- SMTPS, IMAPS (secure email protocols)  
- VPN connections  

### How TLS works (simplified)
1. A client wants to connect securely to a server (e.g., `https://kalilinux.org`).  
2. TLS establishes a **secure session** using a handshake (negotiates encryption algorithms and exchanges keys).  
3. Application data is encrypted and sent over the secure channel.  
4. Connection is closed securely when the session ends.  

---

## 🎯 Objective
- Capture live **TLS-encrypted network packets** and identify TLS behavior and handshake process.  

- **Task:** Generate HTTPS/TLS traffic (e.g., browse a website) and analyze it with Wireshark.  
- **Focus:** Observe TLS handshake, cipher negotiation, and encrypted data exchange.  

---

## 🛠 Tools Used
- **Wireshark** (GUI-based packet capture tool).  
- **Browser / curl / wget** to generate HTTPS traffic.  

---

## 📂 Deliverables
1. **Packet capture file (.pcap)** containing TLS traffic.  
2. **Short report** summarizing TLS handshake, encryption, and packet details.  

---

## 🧭 Steps to Capture Packets

### 1. Traffic Generation
1. Start Wireshark and capture traffic on your active network interface.  
2. Open a browser and visit an HTTPS website, e.g., `https://kalilinux.org`.  
3. Let the capture run for ~30–60 seconds, then stop.  

---

### 2. Packet Capture Details

- **Tool used:** Wireshark  
- **Capture filter (optional):** `tcp port 443`  
- **Display filter (for analysis):** `tls`  

**Typical packets to look for:**
- **ClientHello:** Client initiates TLS handshake, lists supported cipher suites.  
- **ServerHello:** Server chooses cipher suite and responds with certificate.  
- **Certificate:** Server sends its digital certificate to authenticate identity.  
- **ClientKeyExchange / ServerKeyExchange:** Key material exchanged securely.  
- **Finished:** Handshake completes; encrypted data exchange begins.  
- **Application Data:** Encrypted HTTP traffic (TLS payload).  

---

### 3. Important TLS Packet Fields (Explained Simply)

| Field / Item           | What it Means in Layman Terms |
|------------------------|------------------------------|
| **Handshake Type**      | Indicates handshake step (ClientHello, ServerHello, Certificate). |
| **Version**             | TLS version used (TLS 1.2, TLS 1.3, etc.). |
| **Cipher Suite**        | Encryption algorithm chosen for this session. |
| **Random / Nonce**      | Random data to prevent replay attacks. |
| **Certificate**         | Server identity information verified by CA. |
| **Encrypted Application Data** | Actual data sent securely (HTTPS traffic). |

---

### 4. Protocol Recognition in Wireshark

- **Protocol column:** usually shows `TLSv1.2`, `TLSv1.3`, or `SSL` if older version.  
- **Info column:** human-friendly summary, e.g.:  
  - `Client Hello`  
  - `Server Hello, Certificate`  
  - `Encrypted Application Data`  
- **Ports:** common TLS port is 443.  

**Useful display filters:**  
- `tls` — show all TLS packets  
- `tls.handshake.type == 1` — ClientHello only  
- `tls.handshake.type == 2` — ServerHello only  
- `tcp.port == 443` — all HTTPS traffic  

---

### 5. Communication Flow (Step-by-Step)

**TLS Handshake Example Flow (simplified):**

1. **Client → Server:** ClientHello (supported ciphers, TLS version)  
2. **Server → Client:** ServerHello (selected cipher, TLS version)  
3. **Server → Client:** Certificate (server identity)  
4. **Client → Server:** ClientKeyExchange (pre-master secret encrypted)  
5. **Server ↔ Client:** Finished messages (handshake done)  
6. **Client ↔ Server:** Encrypted Application Data exchange begins  

> After handshake, all data is encrypted and cannot be read directly in Wireshark without session keys.  

---

### 6. Observations / Notes (What to look for in capture)

- TLS handshake is visible, but application data is encrypted.  
- Check **Cipher Suite** negotiation to see encryption strength.  
- Observe certificate exchange to verify server authenticity.  
- Large payloads are fragmented into multiple TCP segments.  
- Multiple protocols may appear in capture: DNS (UDP), TCP (SYN/ACK), HTTP (encrypted over TLS).  

---

## ✅ Outcome

- Learned how to capture TLS packets with Wireshark.  
- Observed the TLS handshake process (ClientHello → ServerHello → Key Exchange).  
- Identified TLS-specific fields and handshake types.  
- Recognized that application payloads are encrypted and secure.  

---

## 📎 File Included

- `tls_capture.pcap` — contains TLS traffic generated by visiting `https://kalilinux.org`.  

---

## 💡 Quick Wireshark Tips (for beginners)

- Start capture on the interface with your internet connection (Wi-Fi/Ethernet).  
- Use Display Filter `tls` to focus on TLS traffic.  
- To inspect handshake only: `tls.handshake.type == 1` (ClientHello), `tls.handshake.type == 2` (ServerHello).  
- Right-click packet → **Follow → TCP Stream** to view encrypted conversation structure.  
- TLS Application Data cannot be read without session keys, but handshake metadata is visible.  
