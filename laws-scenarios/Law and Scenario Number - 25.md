## **Law 25 — Recreate Yourself**

Interpretation (offensive context):  
Continuously **change identity, tone, and attack style** to avoid pattern detection and correlation. You are not a fixed persona—you are a **shape-shifting operator**.

---

# 🎯 Attack Scenario — _Multi-Persona Sequential Attack (Identity Rotation to Bypass Detection)_

You target the same user multiple times, but each time with a **completely different identity, role, and communication style**, preventing linkage.

**Target:**

> _Lucas Bennett_ — Finance Executive

**Personas (rotated):**

- _Anya Volkov_ — HR Intern (formal)
    
- _Sophie Turner_ — Ops Assistant (casual)
    
- _Irina Kuznetsova_ — IT Support (authoritative)
    

---

# 🔴 Red Team Objective

- Avoid:
    
    - detection via repeated patterns
        
    - user suspicion from repeated contact
        
- Achieve:
    
    - eventual compromise via **identity variation**
        

---

# 🖥️ Lab Setup

### VMs:

- **Kali (Attacker)** — 3GB
    
- **Ubuntu Victim** — 2GB
    

### Network:

- Host-only
    

---

# ⚙️ Operator Workflow

## Phase 1 — First Identity (HR Context — Soft Entry)

```bash
swaks --to lucas@corp.local \
--from anya.v@corp.local \
--server 192.168.56.101 \
--data "Subject: Policy acknowledgment

Hi,

Please review and acknowledge the updated HR policy:

http://192.168.56.101:8080"
```

👉 Likely ignored or low engagement

---

## Phase 2 — Identity Shift (Ops Context — Casual)

```bash
swaks --to lucas@corp.local \
--from sophie.t@corp.local \
--server 192.168.56.101 \
--data "Subject: Quick check

Hey,

Can you quickly check this for me?

http://192.168.56.101:8080"
```

👉 Different tone  
👉 Different context

---

## Phase 3 — Identity Shift (IT Authority — Strong Trigger)

```bash
swaks --to lucas@corp.local \
--from irina.k@corp.local \
--server 192.168.56.101 \
--data "Subject: Account verification required

Hi,

We detected an issue with your account. Please verify here:

http://192.168.56.101:8080"
```

👉 Authority-based trigger

---

## Phase 4 — Payload

```bash
php -S 0.0.0.0:8080
```

---

## Phase 5 — Execution

Target perception:

- receives unrelated messages
    
- does not correlate them
    
- eventually responds to one
    

👉 Identity fragmentation prevents detection

---

# 🛠️ Tooling + Commands

### Multi-identity delivery:

```bash
swaks --to lucas@corp.local --from anya.v@corp.local
```

```bash
swaks --to lucas@corp.local --from sophie.t@corp.local
```

```bash
swaks --to lucas@corp.local --from irina.k@corp.local
```

---

### Hosting:

```bash
php -S 0.0.0.0:8080
```

---

### Logging:

```php
<?php
file_put_contents("hits.txt", $_SERVER['REMOTE_ADDR']."\n", FILE_APPEND);
?>
```

---

# 🧠 Social Engineering Mapping (Hadnagy)

Relevant concepts:

- **Pretext variation**
    
- **Identity masking**
    
- **Behavioral unpredictability**
    

Key principle:

> Consistency exposes you; variation protects you

---

# 🛡️ Detection & Defensive Insight

Indicators:

- same target receiving:
    
    - multiple unrelated requests
        
- different identities with similar links
    
- repeated link structures
    

Mitigation:

- correlate:
    
    - multi-source interactions per user
        
- user training:
    
    - report unusual patterns
        
- email security:
    
    - detect repeated infrastructure usage
        

---

# 📄 Report Artifact

### Title:

> Multi-Persona Social Engineering via Identity Re-Creation

### Include:

- multiple personas
    
- communication differences
    
- attack sequence
    
- analysis:
    
    - why identity variation bypassed detection
        
- impact:
    
    - eventual compromise via persistence
        

---

# ⚠️ Operator Insight

Single identity:

- traceable
    
- predictable
    

Multiple identities:

- fragmented
    
- resilient
    

You are not a person  
You are **a system of personas**

---

