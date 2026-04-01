## **Law 20 — Do Not Commit to Anyone**

Interpretation (offensive context):  
Do not lock yourself into a single pretext, identity, or vector. Maintain **operational flexibility**—if one path fails or creates risk, **pivot immediately** to an alternative without exposing intent.

---

# 🎯 Attack Scenario — _Multi-Vector Pivoting After Failed Pretext_

You attempt an initial approach. If it fails (no response / suspicion), you **switch identity and technique**, targeting the same user through a different angle.

**Personas (rotating):**

- _Sofia Ivanova_ — HR Intern
    
- _Emily Clarke_ — IT Support Assistant
    

---

# 🔴 Red Team Objective

- Avoid:
    
    - repeated failure patterns
        
    - detection due to persistence
        
- Achieve:
    
    - compromise via **alternative vector**
        

---

# 🖥️ Lab Setup

### VMs:

- **Kali (Attacker)** — 3GB
    
- **Ubuntu Victim** — 2GB
    

### Network:

- Host-only
    

---

# ⚙️ Operator Workflow

## Phase 1 — Initial Attempt (Vector A)

### HR-style pretext:

```bash
swaks --to target@corp.local \
--from sofia.i@corp.local \
--server 192.168.56.101 \
--data "Subject: Policy update

Hi,

Please review the updated HR policy here:

http://192.168.56.101:8080"
```

---

## Phase 2 — Failure Detection

Indicators of failure:

- no response
    
- no link interaction
    
- suspicion reported (simulated)
    

👉 Do NOT retry same method

---

## Phase 3 — Pivot Strategy (Vector B)

Switch:

- identity
    
- context
    
- psychological trigger
    

### IT Support pretext:

```bash
swaks --to target@corp.local \
--from emily.c@corp.local \
--server 192.168.56.101 \
--data "Subject: Access issue detected

Hi,

We detected an issue with your account access. Please verify here:

http://192.168.56.101:8080"
```

👉 Different:

- authority
    
- urgency
    
- context
    

---

## Phase 4 — Payload

```bash
php -S 0.0.0.0:8080
```

---

## Phase 5 — Execution

Target:

- ignored HR message
    
- responds to IT authority
    

👉 Same payload  
👉 Different entry point

---

## Phase 6 — Optional Pivot (Vector C)

If needed, switch again:

- curiosity-based (Law 6)
    
- benefit-based (Law 13)
    

👉 Never stay fixed

---

# 🛠️ Tooling + Commands

### Delivery (multiple vectors):

```bash
swaks --to target@corp.local --from sofia.i@corp.local
```

```bash
swaks --to target@corp.local --from emily.c@corp.local
```

---

### Hosting:

```bash
php -S 0.0.0.0:8080
```

---

### Basic tracking (optional):

```php
<?php
file_put_contents("visits.txt", $_SERVER['REMOTE_ADDR']."\n", FILE_APPEND);
?>
```

---

# 🧠 Social Engineering Mapping (Hadnagy)

Relevant concepts:

- **Pretext flexibility**
    
- **Adaptive attack strategy**
    
- **Failure-based adjustment**
    

Key principle:

> If one door doesn’t open, you don’t knock harder—you try another door

---

# 🛡️ Detection & Defensive Insight

Indicators:

- multiple different requests targeting same user
    
- varying identities contacting same target
    
- inconsistent communication sources
    

Mitigation:

- correlate:
    
    - multiple attempts across identities
        
- user training:
    
    - report unusual repeated contact
        
- monitoring:
    
    - behavioral anomalies per user
        

---

# 📄 Report Artifact

### Title:

> Multi-Vector Social Engineering via Adaptive Pretext Pivoting

### Include:

- initial failed attempt
    
- pivot strategy
    
- comparison:
    
    - why second vector worked
        
- credential capture
    
- impact:
    
    - increased success via flexibility
        

---

# ⚠️ Operator Insight

Rigid attackers:

- fail repeatedly
    

Adaptive attackers:

- succeed eventually
    

You are not committed to:

- identity
    
- method
    
- narrative
    

You are committed to:

> the objective

---

