# Wireshark Network Analysis Project

This project explores how network protocols work and how traffic can be captured and analysed using Wireshark. I used a variety of websites and filters to observe different types of communication and gain insights into security implications.

## 🧪 Steps Taken

I started by launching **Wireshark** and selecting the active Wi-Fi interface. I began capturing packets and visited a series of websites to generate different types of traffic:

- [neverssl.com](http://neverssl.com) – to view unencrypted HTTP traffic  
- [example.com](https://example.com) – to observe standard HTTPS behaviour  
- [dnsleaktest.com](https://dnsleaktest.com) – to trigger DNS queries  
- [httpforever.com/echo](http://httpforever.com/echo) – to inspect HTTP headers  
- [badssl.com](https://badssl.com) – to explore SSL/TLS handshakes and certificate issues  

I interacted with each site by clicking links or running tests to produce more packets. Once I had enough data, I stopped the capture and began analysing the traffic using filters.

---

## 📊 Protocol Analysis

I observed several protocols, each representing different layers of communication:

- **DNS** – Domain name resolution  
- **TCP** – Reliable transport layer traffic  
- **HTTP** – Unencrypted web browsing  
- **TLS** – Encrypted traffic (HTTPS)  
- **ARP** – Local network device discovery  

Understanding these helps identify normal vs suspicious network activity.

---

## 🔍 DNS Analysis

- **Filter Used**: `dns`  
- I focused on `dnsleaktest.com` which generated over 20 DNS queries during its test.  
- Responses contained IP addresses of the queried domains.
### DNS Queries (`dnsleaktest.com`)
> 📸 ![DNS Queries](screenshots/dns_queries.png)

---

## 🌐 HTTP Traffic – neverssl.com

- **Filter Used**: `http`  
- I observed HTTP GET requests and full response content.  
- Since the site uses HTTP, both headers and body were visible in plain text.
### HTTP Traffic (`neverssl.com`)
> 📸 ![HTTP GET Response](screenshots/http_get_response.png)
> ![HTTP GET Response](screenshots/http_get_response1.png)

This shows how insecure HTTP can expose sensitive data like login forms.

---

## 🔒 HTTPS/TLS Traffic – example.com & badssl.com

- **Filter Used**: `tls`  
- Observed TLS handshakes including Client Hello and Server Hello  
- Application data was encrypted, but certificate info was visible  
### TLS Handshake (`example.com`)
> 📸 ![TLS Handshake - example.com](screenshots/tls_handshake.png)
> 📸 ![TLS Handshake - example.com](screenshots/tls_handshake1.png)
> ### Invalid Certificate (`badssl.com`)
> 📸![Invalid Certificate - badssl.com](screenshots/invalid_certificate_badssl.png)

---

## 📡 TCP Stream Analysis

Using the `http` filter, I followed a TCP stream from `neverssl.com`. This showed:

- The browser sending a `GET /` request  
- Server responding with `200 OK` and HTML content  
- Headers such as `Content-Type: text/html`  
### TCP Stream Analysis (`neverssl.com`)
📸 ![TCP Stream - neverssl.com](screenshots/tcp_stream_neverssl.png)

This illustrates how unencrypted traffic can be intercepted and analysed.

---

## 🔐 Security Insights & Best Practices

Wireshark helped me spot potentially risky activity like:

- Spikes in traffic  
- Unusual IP connections  
- Unencrypted protocols leaking data  
- Certificate issues  

### Key Security Practices:

- **Network Segmentation** – Limits access within networks (e.g., VLANs)  
- **Multi-Factor Authentication (MFA)** – Adds protection beyond passwords  
- **IDS/IPS** – Detects and blocks malicious traffic (e.g., Snort, Suricata)  
- **SIEM Tools** – Aggregate and analyse logs (e.g., Splunk, Microsoft Sentinel)  
- **User Awareness Training** – Teaches safe browsing and phishing detection  

---

## ⚠️ Challenges Faced

- **Overwhelming traffic in Wireshark** – I solved this by learning to filter by protocols (e.g., `http`, `dns`)  
- **Firewall configuration** – I initially didn’t know what ports to block/allow, but online documentation helped (Windows Defender)

---

## ✅ Results & Takeaways

- Gained confidence using Wireshark to analyse traffic  
- Set up a more secure home network  
- Better understood how attackers exploit unsecured traffic  
- Learned to apply and explain basic cybersecurity measures effectively  

---
