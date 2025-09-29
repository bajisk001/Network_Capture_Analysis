# TCP Capture Analysis

## 1. Overview of TCP
- **TCP (Transmission Control Protocol)** is a core protocol that provides reliable, ordered, and error-checked delivery of data between applications on hosts across an IP network.  
- If DNS is the phonebook, **TCP is the phone call** — it sets up a connection, ensures both sides are ready, guarantees delivery, and then closes the connection.  

**Common applications that use TCP:**  
- Web browsing (HTTP/HTTPS)  
- FTP  
- Many others  

### How TCP works (simplified)
1. Your computer wants to talk to **kalilinux.org** on a service (e.g., web server on port 80 or 443).  
2. TCP creates a connection with a **three-way handshake** so both sides agree to communicate.  
3. Data is exchanged in ordered segments; the receiver acknowledges received bytes.  
4. When finished, the connection is closed cleanly using a **four-way teardown** (or reset if something goes wrong).  

---

## 🎯 Objective
- Capture live **TCP network packets** and identify TCP behaviour and related traffic types.  

- **Task:** Generate TCP traffic (e.g., browse or `curl` a website) and analyze it with Wireshark.  
- **Focus:** Observe the TCP handshake, data transfer, flags, and teardown.  

---

## 🛠 Tools Used
- **Wireshark** (free, GUI-based packet capture tool).  
- **Browser / curl / netcat** to generate TCP traffic.  

## 📂 Deliverables
- **Packet capture file (.pcap):** `tcp_capture.pcap` — contains TCP traffic.
- **Short report:** Summarizes TCP behaviour, packet fields, and identified protocols.

---

## 🧭 Steps to Capture Packets

### 1. Traffic Generation
1. Start Wireshark and begin capture on your active network interface.
2. In a terminal or browser, generate TCP traffic.
3. Let the capture run for ~30–60 seconds while performing the actions, then stop capture.

## 2. Packet Capture Details

- **Tool used:** Wireshark  
- **Capture filter (optional):** `tcp`  
- **Or specific port:** `tcp port 80 or tcp port 443`  
- **Display filter (for analysis):** `tcp`  

**Typical packets to look for:**
- **SYN (client → server)** — start of handshake.  
- **SYN, ACK (server → client)** — server accepts.  
- **ACK (client → server)** — handshake complete.  
- **PSH/ACK and ACK** — data transfer packets.  
- **FIN/ACK or RST** — connection termination or reset.  

---

## 3. Important TCP Packet Fields (Explained Simply)

| Field / Item       | What it Means in Layman Terms |
|--------------------|-------------------------------|
| **Source Port**    | The port on the client machine (ephemeral/random high port). |
| **Destination Port** | The server’s service port (e.g., 80 for HTTP, 443 for HTTPS). |
| **Sequence Number** | Byte position of this segment — helps reorder and track data. |
| **Acknowledgment**  | Shows the next byte the receiver expects (confirms received data). |
| **Flags**           | Control bits that show packet purpose (SYN, ACK, FIN, RST, PSH). |
| **Window Size**     | How many bytes the receiver is willing to accept (flow control). |
| **Checksum**        | Error-check to ensure packet integrity. |
| **Options**         | Extra settings like MSS (max segment size), Window Scaling, Timestamps. |

---

## 4. Protocol Recognition in Wireshark

- **Protocol column:** usually shows `TCP` or an application protocol like HTTP, TLSv1.3 if Wireshark decodes it.  
- **Info column:** contains human-friendly summary, e.g.:  
  - `443 → 52844 [SYN]` (SYN from server/client)  
  - `HTTP/1.1 200 OK` (HTTP response over TCP)  
- **Ports:** common TCP ports: 80 (HTTP), 443 (HTTPS), 22 (SSH), etc.  

**Useful display filters:**
- tcp # show all TCP packets
- tcp.flags.syn == 1 && tcp.flags.ack == 0 # show SYN packets
- tcp.analysis.retransmission # find retransmissions


---

## 5. Communication Flow (Step-by-Step)

### Three-way handshake (connection setup)
1. **SYN:** Client → Server. Client requests a connection and sends initial sequence number (ISN).  
2. **SYN-ACK:** Server → Client. Server acknowledges client’s SYN and sends its own SYN.  
3. **ACK:** Client → Server. Client acknowledges server’s SYN. **Connection established.**  

### Data transfer
- Client and server exchange segments carrying application data (HTTP requests/responses).  
- Each side acknowledges received bytes using ACKs and sequence numbers.  
- Flow control via Window Size; congestion control and retransmissions may occur.  

### Connection termination (normal)
1. **FIN:** One side sends FIN (finish).  
2. **ACK:** Other side acknowledges.  
3. **FIN:** Other side sends FIN.  
4. **ACK:** First side acknowledges → **connection closed.**  

---

## 6. Observations / Notes (What to look for in capture)
- **Handshake timing:** How long does handshake take? (gives rough RTT).  
- **Flags pattern:** SYN → SYN/ACK → ACK, then PSH/ACK data, then FIN/ACK.  
- **Retransmissions:** If you see `tcp.analysis.retransmission`, packets were lost or delayed.  
- **Window size & scaling:** Watch how flow control adjusts for throughput.  
- **MSS & Options:** The Maximum Segment Size negotiated affects payload efficiency.  
- **Encrypted traffic:** For HTTPS (port 443), Wireshark shows TLS packets over TCP — application payload is encrypted.  
- **RST packets:** Abrupt resets indicate errors or services rejecting connections.  
- **Large transfers:** Observe segmentation, multiple packets containing parts of payload.  

---

## ✅ Outcome
- Learned how to capture TCP packets with Wireshark.  
- Observed TCP connection lifecycle: three-way handshake → data transfer → teardown.  
- Identified TCP-specific fields (SYN/ACK, Seq/Ack, Window) and common behaviours (retransmissions, RST/FIN).  
- Recognized related protocols in a live capture (DNS, HTTP/HTTPS, ICMP).  

---

## 📎 File Included
- `tcp.pcap` — contains TCP traffic generated by browsing **kalilinux.org** (handshake, data transfer, teardown).  

---

## 💡 Quick Wireshark Tips (for beginners)
- Start capture on the interface that has your internet connection (Wi-Fi or Ethernet).  
- Use **Display Filter** `tcp` to focus on TCP packets.  
- To view only the handshake for a particular connection:  
- tcp.port == 80 && tcp.flags.syn == 1
- Right-click a packet → **Follow → TCP Stream** to see the full conversation between client and server in readable order.  
- Use `tcp.analysis.time_delta` or **Round Trip Time columns** (enable them) to inspect delays.
