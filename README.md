# Network Traffic Analysis with Wireshark
Wireshark packet capture and analysis project demonstrating DNS, HTTP, HTTPS and ICMP protocols.
## Wireshark
Wireshark is a network analysis tool that examines traffic moving across wired and wireless networks. It captures packets as they travel between devices, allowing users to inspect the details of network communications.  
## Protocol Analysis Summary

### 1. DNS Traffic Analysis (`udp.port == 53`)
<img width="1355" height="559" alt="DNS (UDP)" src="https://github.com/user-attachments/assets/a721848f-2337-4242-b41d-7a794418ce8b" />

**Purpose**: Capture domain name resolution traffic  
**Key Findings**:
- Resolved domains: `wikipedia.org`, `google.com`
- Record types observed:
  - `A` records (IPv4)
  - `AAAA` records (IPv6)
  - `CNAME` aliases (e.g., `wikipedia.org` → `dyna.wikimedia.org`)  

---

### 2. HTTP Traffic Analysis (`http`)
<img width="1359" height="562" alt="http" src="https://github.com/user-attachments/assets/059e8392-9c40-4864-8a57-0fff99627c0f" />

**Purpose**: Examine unencrypted web traffic  
**Key Findings**:
- Request/Response pairs captured:
  - `GET /projex.htm HTTP/1.1` → `200 OK` (success)
  - `GET /archives/2013/...` → `404 Not Found` (error)
  - Multiple `304 Not Modified` responses (cached content)
- Headers:
  - User-Agent strings
  - Server responses with content types (e.g., `text/html`)

---

### 3. HTTPS/TLS Analysis (`tls`)
<img width="1363" height="556" alt="TLS" src="https://github.com/user-attachments/assets/6f68ba63-34fc-42fe-a7a7-b5194d9282b6" />

**Purpose**: Inspect encrypted web traffic  
**Key Findings**:
- TLS 1.3 handshake observed with `www.google.com`:
  1. `Client Hello` (SNI: `www.google.com`)
  2. `Server Hello` (Cipher suite negotiation)
  3. `Application Data` (Encrypted content)
- Port 443 traffic verified

---

### 4. ICMP Analysis (`icmp`)
<img width="1353" height="542" alt="ICMP" src="https://github.com/user-attachments/assets/44571ce8-298d-4baa-bbcf-12717a1cad0a" />

**Purpose**: Test network connectivity  
**Key Findings**:
- Ping exchange with `8.8.8.8` (Google DNS):
  - Echo requests (TTL=64)
  - Echo replies (TTL=112)
- Average RTT: 50ms (visible in packet timestamps)

---

### 5. OCSP Traffic (Observed)
**Background Protocol**: Online Certificate Status Protocol  
<img width="1358" height="561" alt="OSCP" src="https://github.com/user-attachments/assets/7961feb5-86bc-421f-ad96-e3bff27052b2" />

**Findings**:
- Automatic certificate validation checks to:
  - `2404:6800:4007:836...` (Google services)
  - `2405:201:c4oe:6699...` (OCSP responder)

---

## Key Technical Takeaways
**Protocol Isolation**: Successfully filtered and analyzed 4 core protocols  
**Real-World Traffic**: Captured both intentional (tested) and background traffic  

**Security Observations**:
  - Contrasted HTTP (plaintext) vs HTTPS (encrypted)  
  - Identified certificate validation via OCSP  

## Files Included
- `capture.pcap`: Raw packet data
- Screenshots: 
  - `dns_traffic.png`  
  - `http_requests.png`  
  - `tls_handshake.png`

## How to Verify
1. Open `capture.pcap` in Wireshark
2. Apply the same filters (e.g., `http`, `tls`)
3. Compare with screenshots for validation
