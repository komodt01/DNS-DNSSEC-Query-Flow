# DNS & DNSSEC Query Flow

## Overview
This repository provides a comprehensive explanation of **how DNS queries work**, incorporating **caching mechanisms** and **DNSSEC validation** for enhanced security.

### **Why This Matters**
- **Caching reduces latency** by storing frequently accessed DNS records.
- **DNSSEC prevents spoofing attacks** by ensuring response authenticity.
- **Optimized query flow** improves performance and security.

---

## **DNS Query Flow with Cache & DNSSEC**
DNS queries follow a structured **hierarchical lookup** process, leveraging **cache** to optimize performance and **DNSSEC** to ensure trust. The flow is outlined below:

### **Query Flow Table**
| Step | Component | Description |
|------|-----------|-------------|
| 1 | **Client (Local Cache)** | The client first checks its **local DNS cache** for the requested domain. If found and TTL has not expired, it returns the cached IP address. |
| 2 | **ISP Resolver Cache** | If not in the local cache, the query is sent to the **ISP’s recursive resolver**, which checks its own cache for the record. |
| 3 | **TTL Expiration Check** | If the resolver has a cached response but its **TTL (Time-To-Live) has expired**, it proceeds to query authoritative DNS servers. |
| 4 | **Root DNS Server** | If no valid cached entry exists, the resolver queries a **Root DNS server**, which directs it to the appropriate **Top-Level Domain (TLD) server** (e.g., `.com`, `.org`). |
| 5 | **TLD Server** | The **TLD server** points the resolver to the **Authoritative Name Server** for the requested domain. |
| 6 | **DNSSEC Validation (If Enabled)** | If DNSSEC is enabled, the resolver checks **digital signatures** to verify the integrity and authenticity of the DNS response. |
| 7 | **Authoritative Name Server** | The **authoritative DNS server** provides the final **IP address** for the requested domain. |
| 8 | **Resolver Caches the Response** | The resolver stores the **retrieved IP address** in its cache for a specified **TTL period**. |
| 9 | **Client Receives the IP Address** | The resolver returns the resolved **IP address** to the client, which then **stores it in its local cache** for future use. |
| 10 | **Client Accesses the Website** | The client uses the resolved IP address to initiate a connection to the destination server. |

---

## **How DNSSEC Enhances Security**
DNSSEC (Domain Name System Security Extensions) adds **cryptographic signatures** to DNS responses, ensuring that data has not been tampered with.

### **How It Works**
1. **The DNS resolver retrieves a DNS record** and checks for a **DNSSEC signature (RRSIG record).**
2. **The resolver validates the signature** against the DNSSEC key (DNSKEY record) of the authoritative server.
3. **If the signature is valid**, the response is considered authentic.
4. **If the signature fails**, the resolver discards the response to prevent spoofing attacks.

### **Key Benefits of DNSSEC**
✅ **Prevents DNS Spoofing** – Ensures data is from an authentic source.  
✅ **Cryptographic Integrity** – Uses public/private key cryptography.  
✅ **Reduces MITM Attacks** – Prevents interception and modification of responses.  

---

## **Conclusion**
This repository provides a **detailed guide** to DNS resolution, emphasizing:
- **Efficient caching strategies** for performance optimization.
- **DNSSEC verification** to mitigate security risks.
- **Step-by-step breakdown of DNS queries**, ensuring a thorough understanding.

---

### **How to Use This Repository**
📌 **Clone the repository**:  
```sh
git clone https://github.com/YOUR_GITHUB_USERNAME/DNS-DNSSEC-Query-Flow.git
