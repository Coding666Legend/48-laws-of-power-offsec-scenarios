## **Law 21 — Play a Sucker to Catch a Sucker**

Interpretation (offensive context):  
Deliberately present as **inexperienced or confused** to trigger the target’s **helper instinct**. People lower guard when they feel superior and become more willing to disclose or assist.

---

# 🎯 Attack Scenario — _Credential Leakage via Induced Assistance (Controlled Incompetence)_

You act as a **struggling junior employee**, prompting the target to **voluntarily reveal access details or workflows**.

**Persona:**

> _Yulia Ivanova_, 20 y/o Finance Intern

---

# 🔴 Red Team Objective

- Extract:
    
    - credential patterns
        
    - access methods
        
    - internal links
        
- Without:
    
    - direct requests
        
    - obvious phishing
        

---

# 🖥️ Lab Setup

### VMs:

- **Kali (Attacker)** — 3GB
    
- **Ubuntu Victim** — 2GB
    

### Network:

- Host-only
    

---

# ⚙️ Operator Workflow

## Phase 1 — Entry as Incompetent User

Initial message:

```bash
swaks --to target@corp.local \
--from yulia.i@corp.local \
--server 192.168.56.101 \
--data "Subject: Need help

Hi,

Sorry if this is basic, I just joined and I’m a bit stuck accessing the finance system."
```

👉 No threat  
👉 No urgency  
👉 Signals vulnerability

---

## Phase 2 — Elicitation via Confusion

Follow-up:

> “It’s asking for login but I’m not sure if it’s the same as email or something different…”

👉 You are not asking:

- “What is your password?”
    

You are prompting:

- explanation
    
- clarification
    

---

## Phase 3 — Target Response (Expected)

Victim may reply:

- “Yes, it’s the same credentials”
    
- “Use your email login here: finance.corp.local”
    

👉 You extract:

- authentication method
    
- internal system details
    

---

## Phase 4 — Optional Escalation

Push slightly:

> “Mine still isn’t working, could you show me how yours looks?”

👉 May lead to:

- screenshots
    
- step-by-step explanation
    

---

## Phase 5 — Transition to Exploit

Once trust is built:

```bash
swaks --to target@corp.local \
--from yulia.i@corp.local \
--server 192.168.56.101 \
--data "Subject: Still stuck

Hi,

I tried again, maybe I’m doing it wrong—does this look like the right page?

http://192.168.56.101:8080"
```

---

## Phase 6 — Payload

```bash
php -S 0.0.0.0:8080
```

---

## Phase 7 — Execution

Target:

- feels helpful
    
- trusts interaction
    
- clicks link
    
- submits credentials
    

👉 They helped you → now they trust you

---

# 🛠️ Tooling + Commands

### Communication:

```bash
swaks --to target@corp.local --from yulia.i@corp.local
```

---

### Logging intel:

```bash
nano intel.txt
```

---

### Hosting payload:

```bash
php -S 0.0.0.0:8080
```

---

# 🧠 Social Engineering Mapping (Hadnagy)

Relevant concepts:

- **Elicitation through indirect questioning**
    
- **Rapport via vulnerability display**
    
- **Helper instinct exploitation**
    

Key principle:

> People reveal more when they think they’re helping

---

# 🛡️ Detection & Defensive Insight

Indicators:

- employees asking:
    
    - basic access questions repeatedly
        
- gradual probing:
    
    - login methods
        
    - system access
        

Mitigation:

- train users:
    
    - “Do not share access methods casually”
        
- enforce:
    
    - official onboarding channels
        
- monitor:
    
    - repeated help-seeking behavior
        

---

# 📄 Report Artifact

### Title:

> Information Extraction via Controlled Incompetence Social Engineering

### Include:

- conversation flow
    
- extracted information
    
- escalation path
    
- credential capture (if executed)
    
- analysis:
    
    - why target complied
        

---

# ⚠️ Operator Insight

Acting smart:

- creates distance
    
- raises suspicion
    

Acting naive:

- builds trust
    
- invites disclosure
    

You are not weak  
You are **strategically incompetent**

---

