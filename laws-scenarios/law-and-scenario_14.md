## **Law 14 — Pose as a Friend, Work as a Spy**

Interpretation (offensive context):  
Adopt a **trusted, friendly identity** to establish rapport, then **covertly extract sensitive information over time**. This is not a one-shot attack—it’s **progressive intelligence gathering**.

---

# 🎯 Attack Scenario — _Covert Information Harvest via Friendly Insider Persona_

You embed yourself as a **helpful colleague**, gradually extracting internal data without triggering suspicion.

**Persona:**

> _Alina Petrova_, 20 y/o Operations Intern

---

# 🔴 Red Team Objective

- Collect:
    
    - internal URLs
        
    - system names
        
    - credential patterns
        
- Enable:
    
    - future targeted attacks (phishing, lateral movement)
        

---

# 🖥️ Lab Setup

### VMs:

- **Kali (Attacker)** — 3GB
    
- **Ubuntu Victim** — 2GB
    

### Network:

- Host-only
    

---

# ⚙️ Operator Workflow

## Phase 1 — Friendly Entry (Rapport Initiation)

You initiate casual interaction:

> “Hey, I just joined the operations team—still figuring things out 😅”

👉 No requests  
👉 Pure relationship building

---

## Phase 2 — Low-Risk Questions (Information Seeding)

Gradually ask harmless questions:

> “Do you usually access reports via the finance portal or something else?”

👉 You extract:

- system names
    
- workflows
    

---

## Phase 3 — Targeted Elicitation

Escalate slightly:

> “Mine keeps asking for a different login… is it the same company credentials?”

👉 You probe:

- authentication methods
    
- credential reuse patterns
    

---

## Phase 4 — Passive Collection

You are not pushing links yet  
You are building:

- knowledge
    
- trust
    
- behavioral profile
    

---

## 🛠️ Tooling + Commands

### 1. Logging Extracted Info

```bash
nano intel.txt
```

Store:

```text
Finance portal: finance.corp.local
Login type: same as email
User behavior: helpful, responsive
```

---

### 2. (Optional OSINT augmentation)

```bash
theHarvester -d corp.local -l 50
```

---

### 3. Later Stage (Optional Exploitation)

Once trust is built:

```bash
php -S 0.0.0.0:8080
```

👉 But only after sufficient rapport

---

## Phase 5 — Expected Result

- You gather:
    
    - internal structure
        
    - authentication patterns
        
    - user behavior
        

👉 No alarms triggered  
👉 No obvious attack

---

# 🧠 Social Engineering Mapping (Hadnagy)

Relevant concepts:

- **Elicitation** → extracting info without direct asking
    
- **Rapport building**
    
- **Information layering**
    

Key principle:

> The best intelligence is given voluntarily

---

# 🛡️ Detection & Defensive Insight

Indicators:

- employees sharing internal info casually
    
- repeated “new employee” questions
    
- gradual probing patterns
    

Mitigation:

- train users:
    
    - “Don’t share internal system details casually”
        
- enforce:
    
    - need-to-know basis
        
- monitor:
    
    - unusual internal conversations
        

---

# 📄 Report Artifact

### Title:

> Covert Intelligence Gathering via Friendly Insider Persona

### Include:

- conversation scripts
    
- extracted intelligence
    
- progression timeline
    
- analysis:
    
    - how trust enabled disclosure
        
- impact:
    
    - reconnaissance for future attacks
        

---

# ⚠️ Operator Insight

Direct attacks:

- noisy
    
- detectable
    

Covert intel gathering:

- silent
    
- powerful
    
- foundational
    

You’re not attacking yet  
You’re **preparing the battlefield**

---

