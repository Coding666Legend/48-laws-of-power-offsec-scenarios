## **Law 6 — Court Attention at All Costs**

Interpretation (offensive context):  
If the target doesn’t engage, the attack fails. You must **win the attention battle first**, then deliver the payload. This is about **click inducement engineering**.

---

# 🎯 Attack Scenario — _Curiosity-Driven Click Hijack (Attention Exploit)_

You craft a message that **forces interaction** through curiosity, surprise, or perceived relevance.

**Persona:**

> _Daria Morozova_, 20 y/o Marketing Intern

---

# 🔴 Red Team Objective

- Maximize:
    
    - **open rate**
        
    - **click-through rate (CTR)**
        
- Achieve:
    
    - payload interaction (link click)
        

---

# 🖥️ Lab Setup

### VMs:

- **Kali (Attacker)** — 3GB
    
- **Ubuntu Victim** — 2GB
    

### Network:

- Host-only
    

---

# ⚙️ Operator Workflow

## Phase 1 — Attention Engineering

You design the **hook**, not the payload.

### High-performing patterns:

- curiosity gap
    
- personal relevance
    
- mild ambiguity
    

---

## Phase 2 — Subject Line Weaponization

Examples:

- “You were mentioned in this report”
    
- “Is this about you?”
    
- “Check this before it’s finalized”
    

👉 These force:

- immediate attention
    
- emotional engagement
    

---

## Phase 3 — Message Body (keep it light)

> “Not sure if this was meant to include you, but saw your name here.”

Link:

```
http://192.168.56.101:8080
```

👉 No explanation → forces click

---

## Phase 4 — Payload Delivery

Reuse phishing infra:

```bash
php -S 0.0.0.0:8080
```

---

## 🛠️ Tooling + Commands

### 1. High-CTR Email Delivery

```bash
swaks --to target@corp.local \
--from daria.m@corp.local \
--server 192.168.56.101 \
--data "Subject: You were mentioned in this report

Not sure if this was meant to include you, but saw your name here:

http://192.168.56.101:8080"
```

---

### 2. (Optional Enhancement — Tracking Clicks)

Basic logging via PHP:

```php
<?php
file_put_contents("clicks.txt", $_SERVER['REMOTE_ADDR']."\n", FILE_APPEND);
?>
```

👉 Measures engagement

---

## Phase 5 — Execution

Target behavior:

- curiosity triggered
    
- clicks link immediately
    
- engages with payload
    

👉 Attention → Action

---

# 🧠 Social Engineering Mapping (Hadnagy)

Relevant concepts:

- **Curiosity exploitation**
    
- **Emotional triggers** (fear of missing out, concern)
    
- **Cognitive bias** → “I need to check this”
    

Key principle:

> Attention precedes compromise

---

# 🛡️ Detection & Defensive Insight

Indicators:

- vague but provocative subject lines
    
- lack of context
    
- emotional manipulation patterns
    

Mitigation:

- user training:
    
    - “Curiosity is a primary attack vector”
        
- email filtering:
    
    - flag ambiguous high-trigger phrases
        
- sandbox links before access
    

---

# 📄 Report Artifact

### Title:

> High Engagement Phishing via Curiosity-Based Attention Hijacking

### Include:

- subject line variations
    
- CTR comparison (if simulated)
    
- explanation of psychological triggers
    
- captured interaction logs
    

---

# ⚠️ Operator Insight

No attention → no compromise

Technical payload quality is irrelevant if:

- email is ignored
    
- link is not clicked
    

Your first exploit is:

> the human attention system

---

