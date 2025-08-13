# Network Traffic Analysis with Wireshark
Wireshark packet capture and analysis project demonstrating DNS, HTTP, HTTPS, TCP, UDP and ICMP protocols.

## Protocol Analysis Summary

### 1. DNS Traffic Analysis (`udp.port == 53`)

**Purpose**: Capture domain name resolution traffic  
**Key Findings**:
- Resolved domains: `wikipedia.org`, `google.com`
- Record types observed:
  - `A` records (IPv4)
  - `AAAA` records (IPv6)
  - `CNAME` aliases (e.g., `wikipedia.org` → `dyna.wikimedia.org`)
- **Example**: Packet #960 shows DNS query for `www.wikipedia.org`

---

### 2. HTTP Traffic Analysis (`http`)
**Purpose**: Examine unencrypted web traffic  
**Key Findings**:
- Request/Response pairs captured:
  - `GET /projex.htm HTTP/1.1` → `200 OK` (success)
  - `GET /archives/2013/...` → `404 Not Found` (error)
  - Multiple `304 Not Modified` responses (cached content)
- Visible headers:
  - User-Agent strings
  - Server responses with content types (e.g., `text/html`)

---

### 3. HTTPS/TLS Analysis (`tls`)
**Purpose**: Inspect encrypted web traffic  
**Key Findings**:
- TLS 1.3 handshake observed with `www.google.com`:
  1. `Client Hello` (SNI: `www.google.com`)
  2. `Server Hello` (Cipher suite negotiation)
  3. `Application Data` (Encrypted content)
- Port 443 traffic verified

---

### 4. ICMP Analysis (`icmp`)
**Purpose**: Test network connectivity  
**Key Findings**:
- Ping exchange with `8.8.8.8` (Google DNS):
  - Echo requests (TTL=64)
  - Echo replies (TTL=112)
- Average RTT: ~50ms (visible in packet timestamps)

---

### 5. OCSP Traffic (Observed)
**Background Protocol**: Online Certificate Status Protocol  
**Findings**:
- Automatic certificate validation checks to:
  - `2404:6800:4007:836...` (Google services)
  - `2405:201:c4oe:6699...` (OCSP responder)

---

## Key Technical Takeaways
✔ **Protocol Isolation**: Successfully filtered and analyzed 4 core protocols  
✔ **Real-World Traffic**: Captured both intentional (tested) and background traffic  
✔ **Security Observations**: 
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
