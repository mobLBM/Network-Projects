# PayFast Security & Network Design (Packet Tracer)

This repository documents a **security-focused network design** for **PayFast** (a fintech payment platform). It includes a segmented VLAN architecture, secure services (HTTPS + email), a DMZ for a public API server, and a site-to-site IPsec VPN between HQ and a new branch.

---

## Company context
**Company:** PayFast  
**Business model:** transaction-fee + premium subscription (fintech platform for small online businesses).  
**Critical services:** payment gateway, merchant dashboard/reporting, fraud detection & monitoring, public API/SDKs, settlement & reconciliation, KYC/onboarding.  

---

## Key threats & risk focus
High-risk items addressed in this design include:
- Payment data breach
- Fraudulent transactions / account takeover
- API DDoS / availability loss
- Ransomware / infrastructure compromise  
(plus insider threat, third-party compromise, and misconfiguration/human error).

**Initial annual security budget (estimate):** **$55,000**.

---

## Network architecture (segmentation)
The internal network is segmented by business unit using VLANs/subnets:

| VLAN | Department | Subnet | Default Gateway |
|---:|---|---|---|
| 10 | Finance / Treasury | 192.168.10.0/24 | 192.168.10.1 |
| 20 | IT / Development | 192.168.20.0/24 | 192.168.20.1 |
| 30 | Analytics / Data | 192.168.30.0/24 | 192.168.30.1 |
| 40 | Security & Compliance | 192.168.40.0/24 | 192.168.40.1 |
| 50 | Customer Support / Operations | 192.168.50.0/24 | 192.168.50.1 |
| 60 | Sales & Marketing | 192.168.60.0/24 | 192.168.60.1 |

> Note: ACL rules were initially created to restrict inter-department traffic, but were later removed to simplify expansion and reduce conflicts when adding branch/VPN policies.

---

## Services & security controls implemented
### 1) HTTPS-only web server (internal)
- Web server IP: **192.168.20.10**
- HTTPS enabled; HTTP restricted

### 2) Secure email service (internal)
Best-practice controls included:
- strong password policy (admin + users)
- port restrictions (SMTP 25, POP3 110, IMAP 143)
- router ACLs permitting only required mail traffic
- authentication for sending/receiving mail

### 3) Branch expansion + site-to-site IPsec VPN
- New branch server VLAN gateway: **192.168.70.1**
- Site-to-site IPsec VPN (AES for confidentiality + SHA/HMAC for integrity)
- Pre-shared keys for router authentication
- Static routes and crypto maps applied to secure matching traffic across the WAN serial link

### 4) DMZ + Zone-Based Policy Firewall (ZBF)
An external **Public API HTTPS server** is placed in a **DMZ** and protected by ZBF:
- **INSIDE → OUTSIDE:** allow internal hosts to reach the external server (e.g., ICMP ping for validation)
- **OUTSIDE → INSIDE:** block all inbound traffic to internal LANs

**Example interface/zone summary**
- HQ Router: G0/0 (OUTSIDE/DMZ) **10.2.2.1**, G0/1 (INSIDE), S0/0/0 (VPN) **10.1.1.1**
- Branch Router: G0/0 (INSIDE) **192.168.50.1**, S0/0/0 (VPN) **10.1.1.2**
- DMZ HTTPS server: **10.2.2.2**

### 5) Wireless network (secure)
- Wireless VLAN **100** added as INSIDE
- **WPA2-Enterprise** configured with a **RADIUS server**
- Users authenticate with personal credentials (better control vs shared passwords)

---

## Files (repo layout)
```
.
├─ docs/
│  └─ Payfast Security Report final.pdf.pdf
├─ packet-tracer/
│  └─ (your .pkt file here, if you add it)
├─ screenshots/
│  └─ (pings, routing tables, firewall verification, vpn verification)
└─ README.md
```

---

## How to validate (recommended)
### Connectivity & routing
- Ping within each VLAN
- Ping across VLANs (as allowed)
- Verify branch ↔ HQ reachability through the VPN

### Router checks
```
show ip interface brief
show ip route
show crypto isakmp sa
show crypto ipsec sa
show running-config
```

### Firewall (ZBF) checks
- Confirm OUTSIDE→INSIDE traffic is blocked
- Confirm INSIDE→OUTSIDE permitted flows work as expected
- Review logs (if available in your Packet Tracer setup)

### Web & Email checks
- Confirm **HTTPS works** and **HTTP is restricted**
- Confirm mail ports are reachable only from authorized VLANs

---

## Notes
This project is built to support security and compliance expectations for a fintech environment (e.g., PCI DSS), using practical network controls: segmentation, controlled exposure via DMZ, encrypted site-to-site connectivity, and stronger wireless authentication.

