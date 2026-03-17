## **Law 2 — Never Trust Friends Too Much**

Interpretation (offensive context):  
Exploit **informal trust channels**. People lower their guard with familiar identities—this is a primary vector for **lateral movement and credential harvesting**.

---

# 🎯 Attack Scenario — _Internal Impersonation via Trust Pivot_

You compromise (or simulate compromise of) a **low-privilege employee account** and use it to socially engineer a colleague into exposing sensitive access.

**Persona:**

> _Emily Carter_, 20 y/o HR Assistant (trusted internal contact)

---

# 🔴 Red Team Objective

- Achieve **lateral movement** using internal trust
    
- Extract:
    
    - credentials
        
    - internal URLs / portals
        
    - document access
        

---

# 🖥️ Lab Setup (lightweight, controlled)

### VMs:

- **Kali (Attacker)** — 3GB RAM
    
- **Ubuntu Victim 1 (Emily - compromised identity)** — 2GB
    
- **Ubuntu Victim 2 (Target employee)** — 2GB
    

### Network:

- Host-only network
    
- Simulated “internal chat/email” (basic mail or terminal messaging)
    

---

# ⚙️ Operator Workflow

## Phase 1 — Initial Foothold (Simulated)

Assume:

- You already have access to:
    
    ```
    emily.carter@corp.local
    ```
    

👉 This is your **trust anchor**

---

## Phase 2 — Target Selection

Create internal structure:

```id="5z6m4m"
Name, Role
Emily Carter, HR Assistant
Olivia Bennett, Finance Executive
```

Target:

> Olivia Bennett (likely access to financial systems)

---

## Phase 3 — Trust-Based Pretext

You **do NOT act like attacker**  
You act like **colleague asking for small help**

### Script:

> “Hey Olivia, quick one — I’m updating employee records and I can’t access the finance portal link you shared last week… could you send it again?”

Key design:

- casual tone
    
- no urgency spike
    
- familiarity assumed
    

---

## Phase 4 — Escalation (Credential Harvest Variant)

Follow-up:

> “Also it’s asking me to log in again, is it the same credentials or something different? Mine keeps failing.”

👉 This nudges target into:

- revealing login pattern
    
- possibly sharing credentials
    

---

## 🛠️ Tooling + Commands

### 1. Internal Email Simulation

Install mail utils on victim VM:

```bash
sudo apt install mailutils -y
```

Send internal-style message:

```bash
echo "Hey Olivia, quick one — I can’t access the finance portal link you shared last week, could you send it again?" | mail -s "Quick help" olivia@corp.local
```

---

### 2. Fake Internal Portal (Credential Capture)

On Kali:

```bash
mkdir portal && cd portal
```

Create simple phishing page:

```html
<form action="login.php" method="POST">
<input type="text" name="user">
<input type="password" name="pass">
<input type="submit">
</form>
```

Start server:

```bash
php -S 0.0.0.0:8080
```

---

### 3. Deliver Link via Trusted Identity

```bash
echo "Here’s the link I was trying: http://192.168.56.101:8080 — does this look right?" | mail -s "Portal link" olivia@corp.local
```

👉 Trust bypasses suspicion.

---

## Phase 5 — Expected Result

Target:

- clicks link
    
- enters credentials
    
- assumes legitimacy due to internal sender
    

👉 You achieve **credential capture + lateral access**

---

# 🧠 Social Engineering Mapping (Hadnagy)

Relevant concepts:

- **Familiarity bias** → internal identity lowers defenses
    
- **Pretexting** → normal workplace interaction
    
- **Elicitation** → indirect credential extraction
    

Critical principle:

> People don’t verify what feels routine

---

# 🛡️ Detection & Defensive Insight

Indicators:

- Internal accounts sending unusual requests
    
- Links to **non-corporate hosts (IP-based URLs)**
    
- Credential prompts outside official SSO
    

Mitigation:

- Internal phishing awareness
    
- Zero Trust:
    
    - “Never trust internal by default”
        
- Email filtering:
    
    - flag IP-based links
        

---

# 📄 Report Artifact

### Title:

> Lateral Movement via Internal Trust Exploitation

### Include:

- Attack chain:
    
    - compromised identity → trust exploitation → credential capture
        
- Email transcripts
    
- Phishing page screenshot
    
- Captured credentials (lab only)
    
- Impact:
    
    - internal pivot → data access
        

---

# ⚠️ Operator Insight

External attacks require:

- bypassing defenses
    

Internal attacks require:

- **not triggering suspicion**
    

Trust is your stealth layer.

---

