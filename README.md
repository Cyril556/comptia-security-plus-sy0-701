# CompTIA Security+ SY0-701 — Study Notes & Cheat Brain

![CompTIA](https://img.shields.io/badge/CompTIA-Security%2B_SY0--701-red?style=flat-square)
![Domains](https://img.shields.io/badge/Domains-5_of_5_Covered-brightgreen?style=flat-square)
![Score](https://img.shields.io/badge/Practice_Scores-88--90%25-blue?style=flat-square)
![Status](https://img.shields.io/badge/Exam-In_Progress-orange?style=flat-square)

Personal study notes, trigger-based quick reference cards, PBQ walkthroughs, and exam strategy built while preparing for the **CompTIA Security+ SY0-701** exam. Structured for fast review, not re-reading.

---

## Contents

| Section | Description |
|---------|-------------|
| [Domain Weightings](#domain-weightings) | Official exam blueprint |
| [Cheat Brain — Quick Reference Card](#cheat-brain--quick-reference-card) | Trigger-based decision rules for exam questions |
| [IR Phases](#ir-phases--mnemonic) | Incident Response sequence + mnemonic |
| [Ports & Protocols](#ports--protocols) | Essential ports for exam |
| [Cryptography Reference](#cryptography-reference) | Algorithm to use-case mapping |
| [Threat Actor Types](#threat-actor-types) | Identify by motive, not by action |
| [Network Device Placement](#network-device-placement) | IDS vs IPS vs WAF vs Proxy |
| [Governance Hierarchy](#governance-hierarchy) | Policy → Standard → Procedure → Guideline |
| [PBQ Walkthroughs](#pbq-walkthroughs) | Firewall ACL, Log Analysis, IR Ordering |
| [Practice Test Scores](#practice-test-scores) | Score log across all mock exams |

---

## Domain Weightings

| Domain | Title | Weight |
|--------|-------|--------|
| 1 | General Security Concepts | 12% |
| 2 | Threats, Vulnerabilities & Mitigations | 22% |
| 3 | Security Architecture | 18% |
| 4 | Security Operations | 28% |
| 5 | Security Program Management & Oversight | 20% |

**Passing score:** 750 / 900 (scaled) | **Format:** 90 questions, 90 minutes, up to 6 PBQs

---

## Cheat Brain — Quick Reference Card

### FIRST / NEXT Action Questions
```
"Suspects" / "notices" / "unusual activity"  = ANALYSE first, never disconnect
"Confirmed" / "active attack" / "data leaving" = CONTAIN (isolate/disconnect)
"Breach stopped, now what?"                  = ERADICATE (remove/patch)
"Systems clean, restore?"                    = RECOVER
"After incident, improve?"                   = LESSONS LEARNED
```

### RPO vs RTO
```
RPO = Recovery Point Objective  = How much DATA can you lose?  → Solved by REPLICATION
RTO = Recovery Time Objective   = How long can you be DOWN?    → Solved by HA/FAILOVER

Trigger: "data loss" / "15 minutes of transactions" → RPO → real-time replication
Trigger: "downtime" / "back online" / "uptime"      → RTO → high availability
```

### Compensating Controls
```
MUST: keep service running + reduce risk
ALLOWED:  Deploy IDS/IPS to monitor  ✅
          Restrict IPs / whitelist    ✅
NOT:      Remove/disable service     ❌  (elimination, not compensating)
          "Inform users"              ❌  (awareness, not a control)

Trigger: "patch not yet available" + "reduce risk" = IDS/monitoring or access restriction
```

### SASE Components
```
IN SASE:      CASB, SWG, ZTNA, SD-WAN, FWaaS
NOT SASE:     Hardware firewalls at branch, on-premise storage, physical routers

Trigger: "hardware at branch" in SASE question = eliminate it
```

### SDN Security
```
Control plane  = SDN controller (the brain)
Data plane     = forwards packets (the muscles)

Trigger: any SDN security question → protect the CONTROLLER (auth + access controls)
Encryption in transit is good but NOT the most critical answer
```

### Social Engineering Controls
```
Hierarchy:
1. Formal verification PROCESS (callback, verify via IT)  ✅ strongest
2. Security awareness training                            ✅
3. Caller ID / email filters                              ❌ easily spoofed

Trigger: vishing/pretexting → answer = verification PROCESS, never caller ID
```

### SELECT TWO Elimination Rule
```
Step 1: Eliminate operational/IT efficiency options (cost, integration, ease of use)
Step 2: Eliminate factually incorrect options ("one global standard covers all" = false)
Step 3: Pick the two most FOUNDATIONAL security options remaining

Common traps:
- "Seamless integration"     = IT concern, not security ❌
- "Time-based access"        = supplementary, not foundational ❌
- "Employee positioning"     = usability tip, not security ❌
- "Single global standard"   = factually wrong ❌
```

### Third-Party Risk Transfer
```
Only two criteria matter:
1. Financial stability  (can they absorb the risk?)
2. Compliance posture   (do they meet required standards?)

Not relevant: seamless integration, cost savings, technical compatibility
```

### Automation as Workforce Multiplier
```
Multiplier = makes existing humans MORE effective

Trigger: "leverage automation as workforce multiplier"
→ TRAIN humans to do higher-order work (analysis, strategy, threat hunting)
→ NOT outsourcing (removes humans entirely)
```

---

## IR Phases & Mnemonic

**Mnemonic:** Pretty Intelligent Analysts Contain Every Risk Like Pros

```
P - Preparation
I - Identification (Detection)
A - Analysis
C - Containment
E - Eradication
R - Recovery
L - Lessons Learned (Post-Incident)
```

| Phase | Trigger Word in Question |
|-------|-------------------------|
| Preparation | "policy," "plan," "training before incident" |
| Identification | "alert triggered," "anomaly noticed" |
| Analysis | "suspects," "investigating," "confirming scope" |
| Containment | "confirmed breach," "isolate," "disconnect" |
| Eradication | "remove malware," "patch," "wipe system" |
| Recovery | "restore," "bring back online," "test functionality" |
| Lessons Learned | "after the incident," "improve process," "update playbook" |

---

## Ports & Protocols

| Port | Protocol | Service | Notes |
|------|----------|---------|-------|
| 20/21 | TCP | FTP | Cleartext — always replace with SFTP |
| 22 | TCP | SSH / SFTP | Encrypted shell and file transfer |
| 23 | TCP | Telnet | Cleartext — always deny |
| 25 | TCP | SMTP | Email sending |
| 53 | UDP/TCP | DNS | UDP for queries, TCP for zone transfers |
| 80 | TCP | HTTP | Unencrypted web |
| 110 | TCP | POP3 | Email retrieval |
| 143 | TCP | IMAP | Email retrieval with sync |
| 443 | TCP | HTTPS | Encrypted web |
| 445 | TCP | SMB | Windows file sharing — restrict externally |
| 3389 | TCP | RDP | Remote desktop — restrict heavily |
| 3306 | TCP | MySQL | Database — block from Internet |
| 8080 | TCP | HTTP Alt | Alternate web port |
| 161/162 | UDP | SNMP | 161 = queries, 162 = traps |
| 389 | TCP | LDAP | Directory services |
| 636 | TCP | LDAPS | Encrypted LDAP |
| 1433 | TCP | MSSQL | Microsoft SQL Server |

---

## Cryptography Reference

| Algorithm | Type | Use Case |
|-----------|------|----------|
| AES | Symmetric | Bulk data encryption (at rest, in transit) |
| 3DES | Symmetric | Legacy encryption (being phased out) |
| RSA | Asymmetric | Key exchange, digital signatures |
| ECC | Asymmetric | Key exchange, mobile/IoT (smaller keys, same strength) |
| Diffie-Hellman | Key Exchange | Securely exchange keys over insecure channel |
| SHA-256 | Hashing | Integrity verification (one-way, no decryption) |
| MD5 | Hashing | Legacy hash (broken for security use) |
| HMAC | Hashing + Auth | Integrity AND authentication combined |
| PKI / X.509 | Infrastructure | Certificate-based trust and authentication |

**Avalanche effect:** A tiny change in plaintext = massively different ciphertext. Sign of a strong cipher.

**Data states:**
```
At rest    = stored on disk/DB        → AES encryption, access controls
In transit = moving over network      → TLS, VPN, HTTPS
In use     = being processed in RAM   → Secure enclaves, application controls
```

---

## Threat Actor Types

| Actor | Primary Motive | Clue Words |
|-------|---------------|------------|
| Nation-state | Geopolitical, strategic intelligence | "government," "strategic plans," "executive comms intercepted" |
| Cybercriminal | Financial gain, ransomware | "ransom," "sell data," "financial extortion" |
| Hacktivist | Disruption, chaos, ideology | "no data stolen," "no ransom," "timed to event," "cause disruption" |
| Insider threat | Financial, revenge, ideology | "employee," "trusted access," "internal" |
| Corporate spy | Competitive advantage | "competitor," "trade secrets," "R&D stolen" |
| Script kiddie | Recognition, thrill | "unsophisticated tools," "no clear motive" |

**Key triggers:**
- No ransom + no data + timed to event = **Hacktivist**
- Trade secrets + strategic comms = **Corporate spy + Nation-state**

---

## Network Device Placement

```
Internet
   |
[Firewall]        ← between Internet and DMZ; and between DMZ and LAN
   |
  DMZ
  [WAF]           ← in front of web server specifically
  [Web Server]
   |
[IPS]             ← inline, actively blocks traffic
   |
[Internal LAN]
[SIEM]            ← inside LAN, collects logs from everything
[Proxy]           ← between internal users and Internet

IDS              = PASSIVE, monitor only, SPAN port (never inline)
IPS              = ACTIVE, inline, blocks traffic
WAF              = web app traffic only, in front of web server
Proxy            = intercepts outbound user traffic
SIEM             = log aggregation and correlation, inside LAN
```

---

## Governance Hierarchy

```
Policy     (What — mandatory, high-level)
   ↓
Standard   (Specific mandatory technical requirements, e.g., AES-256 only)
   ↓
Procedure  (Step-by-step how to implement)
   ↓
Guideline  (Recommended, NOT mandatory)

Trigger: "defines specific mandatory technical requirements" → STANDARD
Trigger: "optional / recommended" → GUIDELINE
Trigger: "high-level organisational direction" → POLICY
```

---

## SOAR

```
SOAR = Security Orchestration, Automation and Response

- Automates repetitive tasks (alert triage, ticket creation, IOC lookup)
- Uses PLAYBOOKS (automated workflows for specific incident types)
- Frees analysts for higher-order work

Trigger: "reduce analyst alert fatigue" → SOAR
Trigger: "automate IR workflow" → SOAR
Trigger: "workforce multiplier" → SOAR enables this
```

---

## PBQ Walkthroughs

### Firewall ACL — How to Build a Rule Table

**Given requirements:**
- Allow HTTPS inbound to web server at 10.0.0.5
- Allow SSH from admin only (10.0.0.10)
- Allow DNS outbound from internal network
- Block everything else

**Correct rule table:**

| Rule | Source | Destination | Protocol | Port | Action |
|------|--------|-------------|----------|------|--------|
| 1 | ANY | 10.0.0.5 | TCP | 443 | ALLOW |
| 2 | 10.0.0.10 | 10.0.0.5 | TCP | 22 | ALLOW |
| 3 | 10.0.0.0/24 | DNS_Server | UDP | 53 | ALLOW |
| 4 | ANY | ANY | ANY | ANY | DENY |

**Rules:**
- Specific ALLOW rules first
- Implicit DENY always last
- Never ANY-ANY-ALLOW
- Use specific IPs not subnet ranges unless stated

### Log Analysis — Attack Identification

| Log Pattern | Attack Type | First Response |
|-------------|------------|----------------|
| Repeated SYN, no ACK, high volume | DoS / SYN Flood | Block source IP at firewall |
| Multiple auth failures same IP | Brute Force | Lock account, block IP |
| Outbound to unknown IP at odd hours | C2 / Exfiltration | Contain (disconnect from network) |
| Sequential port hits (1,2,3,4...) | Port Scan / Recon | Log and monitor; alert SOC |
| "SELECT" or "OR 1=1" in app logs | SQL Injection | Block request; patch input validation |
| DNS queries to unusual domains | DNS Exfiltration / C2 | Block domain; investigate endpoint |

### IR Ordering — Drag and Drop

```
Correct order:
1. Prepare (policies, tools, team)
2. Detect & Identify (alert, anomaly confirmed)
3. Analyse (scope, confirm, investigate)
4. Contain (isolate affected systems)
5. Eradicate (remove threat, patch)
6. Recover (restore, test, monitor)
7. Post-Incident (report, lessons learned, update playbook)
```

---

## Practice Test Scores

| # | Source | Score | PBQs | Notes |
|---|--------|-------|------|-------|
| 1 | Dion (YouTube) | 88% (failed <10/90) | None | Pre-Domain 4&5 study |
| 2 | CertPreps | 79% (55/70 completed) | None | Time management issue |
| 3 | Dion #2 | 88% (failed 11/90) | None | |
| 4 | Pearson Test Prep #1 | 90% (failed 9/90) | None | Best score to date |

**Target:** 85%+ consistently across 2-3 different providers before exam day.

---

## Resources Used

- Professor Messer SY0-701 Course (primary video resource)
- Mike Chapple & David Seidl — CompTIA Security+ Study Guide SY0-701
- Pearson Test Prep (official practice exams)
- Dion Training practice exams (via YouTube)
- Immersive Labs — Cyber Million: Defensive Security Operations
- Custom exam simulator: [SY0-701 Exam Simulator](https://github.com/Cyril556/sy0-701-simulator)
