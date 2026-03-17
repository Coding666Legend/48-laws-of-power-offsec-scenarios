## **Law 15 — Crush Your Enemy Totally**

Interpretation (offensive context):  
Partial compromise leaves room for **detection, recovery, and response**. Once access is achieved, you **chain actions to deepen control and remove recovery paths** (within lab scope).

---

# 🎯 Attack Scenario — _End-to-End Compromise Chain (Credential → Access → Persistence)_

You start with a successful social engineering entry and **extend it into sustained access**, simulating a complete attack lifecycle.

**Persona (initial vector):**

> _Victoria Smirnova_, 20 y/o IT Assistant

---

# 🔴 Red Team Objective

- Move from:
    
    - initial credential capture → **usable access**
        
- Establish:
    
    - persistence (lab-safe simulation)
        
- Extract:
    
    - additional data for lateral movement
        

---

# 🖥️ Lab Setup (slightly expanded but within limits)

### VMs:

- **Kali (Attacker)** — 3GB
    
- **Ubuntu Victim (User)** — 2GB
    
- _(Optional for depth)_ Second Ubuntu — 2GB
    

### Network:

- Host-only
    

---

# ⚙️ Operator Workflow

## Phase 1 — Initial Access (Entry Point)

Reuse phishing flow:

```bash
php -S 0.0.0.0:8080
```

Captured:

```
user:pass
```

👉 This is **not the end**, it’s the entry

---

## Phase 2 — Credential Validation (Critical Step)

Test credentials:

```bash
ssh user@192.168.56.102
```

👉 Validate:

- reuse
    
- access level
    

---

## Phase 3 — Establish Persistence (Lab-safe)

Simulate persistence (no destructive actions)

### Option A — SSH Key Persistence

On Kali:

```bash
ssh-keygen -t rsa
```

Copy key:

```bash
ssh-copy-id user@192.168.56.102
```

👉 Now:

- password no longer needed
    
- persistent access established
    

---

### Option B — Cron-based Persistence (simulation)

```bash
crontab -e
```

Add:

```bash
* * * * * echo "alive" >> /tmp/log.txt
```

👉 Demonstrates:

- scheduled execution capability
    

---

## Phase 4 — Internal Recon (Post-Access)

```bash
whoami
```

```bash
uname -a
```

```bash
ls /home
```

```bash
cat /etc/passwd
```

👉 Identify:

- users
    
- system structure
    

---

## Phase 5 — Data Extraction (Controlled)

```bash
cat ~/documents/report.txt
```

👉 Simulate:

- sensitive file access
    

---

## Phase 6 — Optional Lateral Movement (light)

If second VM exists:

```bash
ssh user2@192.168.56.103
```

👉 Use:

- same credentials
    
- or extracted info
    

---

## 🛠️ Tooling + Commands

### Access:

```bash
ssh user@target
```

### Persistence:

```bash
ssh-copy-id user@target
```

### Recon:

```bash
whoami
id
uname -a
```

### Enumeration:

```bash
cat /etc/passwd
```

---

## Phase 7 — Expected Result

You achieve:

- initial compromise
    
- persistent access
    
- internal visibility
    

👉 This is a **complete chain**, not a single event

---

# 🧠 Social Engineering Mapping (Hadnagy)

Relevant concepts:

- **Initial trust exploitation → entry point**
    
- After that:
    
    - technical exploitation takes over
        

Key principle:

> Social engineering opens the door, technical skill secures the environment

---

# 🛡️ Detection & Defensive Insight

Indicators:

- unusual SSH access
    
- new SSH keys added
    
- unexpected cron jobs
    

Mitigation:

- monitor:
    
    - authorized_keys changes
        
- enforce:
    
    - MFA for SSH
        
- audit:
    
    - cron jobs regularly
        

---

# 📄 Report Artifact

### Title:

> Full Compromise Chain via Social Engineering Initial Access

### Include:

- attack chain diagram:
    
    - phishing → credential → access → persistence
        
- commands executed
    
- persistence method
    
- impact:
    
    - sustained unauthorized access
        

---

# ⚠️ Operator Insight

Most beginners stop at:

- “I got credentials”
    

That’s incomplete.

Real operators:

- convert access → control
    
- control → persistence
    
- persistence → expansion
    

---

