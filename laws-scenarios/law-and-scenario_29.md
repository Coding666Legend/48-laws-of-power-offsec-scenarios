## **Law 29 — Plan All the Way to the End**

Interpretation (offensive context):  
Design the operation **end-to-end before first contact**. Every stage—entry, expansion, persistence, and exit—should be pre-modeled. Ad-hoc execution creates gaps and exposure.

---

# 🎯 Attack Scenario — _Pre-Planned Full Chain (SE → Access → Pivot → Persistence → Exit)_

You predefine a **complete attack lifecycle** against a single target and execute against that plan.

**Target:**

> _Michael Turner_ — Finance Manager

**Persona (initial vector):**

> _Alisa Voronina_, 20 y/o IT Support Intern

---

# 🔴 Red Team Objective

- Achieve:
    
    - initial access
        
    - controlled expansion
        
    - persistence (lab-safe)
        
- Maintain:
    
    - low detection probability
        
- Exit:
    
    - with artifacts and minimal traces (simulated)
        

---

# 🖥️ Lab Setup (fits 16GB)

### VMs:

- **Kali (Attacker)** — 3GB
    
- **Ubuntu Victim (User)** — 2GB
    
- _(Optional)_ Second Ubuntu — 2GB
    

### Network:

- Host-only
    

---

# 🧭 Pre-Plan (before any action)

```text
Stage 1: Initial access (phish)
Stage 2: Credential validation (SSH)
Stage 3: Persistence (SSH key)
Stage 4: Recon (users, files)
Stage 5: Data extraction (controlled)
Stage 6: Optional pivot (second host)
Stage 7: Exit (log review, cleanup simulation)
```

👉 No improvisation during execution

---

# ⚙️ Operator Workflow

## Phase 1 — Initial Access (Planned Entry)

```bash
swaks --to michael@corp.local \
--from alisa.v@corp.local \
--server 192.168.56.101 \
--data "Subject: Account verification

Hi,

We detected an issue with your account. Verify here:

http://192.168.56.101:8080"
```

---

## Phase 2 — Payload

```bash
php -S 0.0.0.0:8080
```

Capture:

```
user:pass
```

---

## Phase 3 — Credential Validation

```bash
ssh user@192.168.56.102
```

👉 Confirm access before proceeding

---

## Phase 4 — Persistence (Pre-planned)

```bash
ssh-keygen -t rsa
ssh-copy-id user@192.168.56.102
```

👉 Ensures continued access

---

## Phase 5 — Recon (Structured)

```bash
whoami
id
uname -a
ls /home
cat /etc/passwd
```

👉 Identify:

- users
    
- system layout
    

---

## Phase 6 — Data Extraction (Defined Scope)

```bash
cat ~/documents/finance.txt
```

👉 Only predefined targets  
👉 Avoid random exploration

---

## Phase 7 — Optional Pivot

```bash
ssh user2@192.168.56.103
```

👉 Only if planned beforehand

---

## Phase 8 — Exit Strategy (Simulated)

- Review:
    
    - logs
        
    - artifacts
        
- Do NOT:
    
    - leave unnecessary traces (conceptual)
        

---

# 🛠️ Tooling + Commands

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
uname -a
cat /etc/passwd
```

### Hosting:

```bash
php -S 0.0.0.0:8080
```

---

# 🧠 Social Engineering Mapping (Hadnagy)

Relevant concepts:

- **Pretext planning**
    
- **attack lifecycle thinking**
    
- SE is only:
    
    - **entry point**, not the full operation
        

Key principle:

> The attack is successful only if the end objective is achieved

---

# 🛡️ Detection & Defensive Insight

Indicators:

- multi-stage behavior:
    
    - phishing → login → SSH access
        
- persistence artifacts:
    
    - new SSH keys
        
- structured recon activity
    

Mitigation:

- monitor:
    
    - authentication + SSH patterns
        
- enforce:
    
    - MFA
        
- audit:
    
    - authorized_keys
        
- detect:
    
    - unusual command sequences
        

---

# 📄 Report Artifact

### Title:

> End-to-End Attack Lifecycle via Planned Social Engineering Entry

### Include:

- full attack chain diagram
    
- each stage with commands
    
- persistence method
    
- data accessed
    
- analysis:
    
    - why planning improved success
        
- impact:
    
    - sustained access + controlled expansion
        

---

# ⚠️ Operator Insight

Unplanned attack:

- chaotic
    
- incomplete
    
- detectable
    

Planned attack:

- structured
    
- efficient
    
- controlled
    

You don’t “try things”  
You **execute a design**

---

