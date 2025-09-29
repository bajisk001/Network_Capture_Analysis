# Wireshark Q&A

---

### 1. What is Wireshark used for?

-   **Layman:**
    Wireshark is like a microscope for your network. It lets you see the data flowing in and out of your computer, like emails, website requests, or game traffic.

-   **Technical:**
    Wireshark is a network protocol analyzer that captures live network traffic and displays packet-level details. It supports protocol dissection, filtering, and analysis, allowing troubleshooting, security audits, and performance monitoring.

---

### 2. What is a packet?

-   **Layman:**
    A packet is like a letter sent through the internet. It contains both the message (data) and the address (where it’s going and coming from).

-   **Technical:**
    A packet is the basic unit of data transmitted over a network. It contains headers (metadata such as source/destination IP, ports, protocol) and payload (actual data). Networks transmit large files by splitting them into multiple packets.

---

### 3. How to filter packets in Wireshark?

-   **Layman:**
    You can tell Wireshark what to show by typing what you want to see. For example, only HTTP traffic or only pings.

-   **Technical:**
    Wireshark supports Display Filters and Capture Filters:
    -   **Display Filter:** Refines which captured packets are visible (e.g., `tcp`, `udp.port == 53`, `icmp`).
    -   **Capture Filter:** Limits which packets are captured in real-time (e.g., `port 80`, `host 192.168.1.1`).

---

### 4. What is the difference between TCP and UDP?

-   **Layman:**
    -   **TCP:** Like a phone call – it connects, talks, confirms, and hangs up. Reliable, ordered.
    -   **UDP:** Like sending postcards – you just send it and hope it reaches. Fast, but not guaranteed.

-   **Technical:**

| Feature       | TCP                             | UDP                             |
| :------------ | :------------------------------ | :------------------------------ |
| **Connection**  | Connection-oriented             | Connectionless                  |
| **Reliability** | Reliable (acknowledgment)       | Unreliable (no ACK)             |
| **Ordering**    | Ordered delivery                | No order guarantee              |
| **Use cases**   | HTTP, FTP, Email                | DNS, VoIP, Streaming            |

---

### 5. What is a DNS query packet?

-   **Layman:**
    It’s a question sent to a DNS server asking: “What’s the IP address of google.com?”

-   **Technical:**
    A DNS query packet is a UDP (or sometimes TCP) packet sent from a client to a DNS server, containing:
    -   Transaction ID (links query ↔ response)
    -   Query Flags (recursion desired, query type)
    -   Question section (domain name and record type)
    
    The server responds with a DNS response packet containing the IP address.

---

### 6. How can packet capture help in troubleshooting?

-   **Layman:**
    It’s like watching the network conversation. You can see if messages are lost, delayed, or going to the wrong place.

-   **Technical:**
    Packet capture helps in:
    -   Identifying packet loss, retransmissions, and delays
    -   Detecting misconfigurations or security issues
    -   Analyzing protocol behavior (TCP handshake, DNS resolution, HTTP requests/responses)
    -   Debugging application/network problems in real time.

---

### 7. What is a protocol?

-   **Layman:**
    A protocol is like a language or set of rules that computers use to talk to each other.

-   **Technical:**
    A protocol is a set of rules and conventions governing how data is transmitted and interpreted across networks. Examples include TCP, UDP, HTTP, DNS, and TLS. Protocols define packet structure, addressing, timing, and error handling.

---

### 8. Can Wireshark decrypt encrypted traffic?

-   **Layman:**
    Wireshark can’t read your secret messages directly, but if you have the keys, it can peek inside encrypted traffic like HTTPS.

-   **Technical:**
    Wireshark can decrypt certain encrypted traffic (e.g., TLS/SSL) if:
    -   You have the private key of the server (for older RSA-based TLS)
    -   Or you capture the pre-master secret from the client browser (for modern TLS using ephemeral key exchange like ECDHE).
    
    Without keys, Wireshark can only show metadata, like IP, ports, and handshake details.
