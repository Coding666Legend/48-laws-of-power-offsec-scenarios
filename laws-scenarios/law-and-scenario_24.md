## **Law 24 — Play the Perfect Courtier**

Interpretation (offensive context):  
Blend into hierarchy by being **polite, deferential, and non-threatening**, especially toward authority figures. You gain access not by force, but by **social positioning and likability**.

---

# 🎯 Attack Scenario — _Authority-Aligned Compliance via Polite Subordinate Persona_

You approach a **high-authority user** and position yourself as a **respectful, low-risk subordinate**, increasing the chance of cooperation.

**Target:**

> _Edward Hastings_ — Senior Finance Director

**Persona:**

> _Katerina Orlova_, 20 y/o Junior Operations Assistant

---

# 🔴 Red Team Objective

- Extract:
    
    - access validation
        
    - credential interaction
        
- Avoid:
    
    - triggering authority skepticism
        
- Use:
    
    - **social hierarchy positioning**
        

---

# 🖥️ Lab Setup

### VMs:

- **Kali (Attacker)** — 3GB
    
- **Ubuntu Victim (HVT)** — 2GB
    

### Network:

- Host-only
    

---

# ⚙️ Operator Workflow

## Phase 1 — Entry with Deference

Initial message:

```bash
swaks --to edward@corp.local \
--from katerina.o@corp.local \
--server 192.168.56.101 \
--data "Subject: Assistance request

Dear Mr. Hastings,

Apologies for the interruption. I’ve been asked to assist with validating some operational processes related to finance, and I wanted to ensure I’m following the correct procedure on your end."
```

👉 Tone:

- respectful
    
- indirect
    
- non-threatening
    

---

## Phase 2 — Alignment with Authority

Follow-up:

> “I believe this involves confirming access via the finance portal, but I didn’t want to proceed without checking with you first.”

👉 You:

- acknowledge authority
    
- request guidance
    
- avoid direct instruction
    

---

## Phase 3 — Guided Action Setup

Now introduce action subtly:

```bash
swaks --to edward@corp.local \
--from katerina.o@corp.local \
--server 192.168.56.101 \
--data "Subject: Confirmation step

Dear Mr. Hastings,

If this is correct, I was advised this is the verification step:

http://192.168.56.101:8080

Please let me know if I’m proceeding correctly.

Thank you,
Katerina"
```

👉 You are not telling  
👉 You are “seeking validation”

---

## Phase 4 — Payload

```bash
php -S 0.0.0.0:8080
```

---

## Phase 5 — Execution

Target:

- feels respected
    
- does not feel challenged
    
- engages with request
    

👉 Compliance via hierarchy

---

# 🛠️ Tooling + Commands

### Communication:

```bash
swaks --to edward@corp.local --from katerina.o@corp.local
```

---

### Hosting:

```bash
php -S 0.0.0.0:8080
```

---

### Optional logging:

```php
<?php
file_put_contents("access.txt", $_SERVER['REMOTE_ADDR']."\n", FILE_APPEND);
?>
```

---

# 🧠 Social Engineering Mapping (Hadnagy)

Relevant concepts:

- **Authority respect**
    
- **Rapport through politeness**
    
- **Indirect elicitation**
    

Key principle:

> People in power respond better to respect than pressure

---

# 🛡️ Detection & Defensive Insight

Indicators:

- overly polite requests from unknown internal identities
    
- indirect action prompts
    
- hierarchical manipulation
    

Mitigation:

- train:
    
    - executives specifically (high-value targets)
        
- enforce:
    
    - verification regardless of tone
        
- monitor:
    
    - unusual respectful-but-actionable requests
        

---

# 📄 Report Artifact

### Title:

> Authority-Based Social Engineering via Subordinate Persona

### Include:

- communication tone analysis
    
- step-by-step interaction
    
- credential capture
    
- analysis:
    
    - how hierarchy influenced compliance
        
- impact:
    
    - compromise of high-value user
        

---

# ⚠️ Operator Insight

Direct requests to authority:

- trigger resistance
    

Subordinate positioning:

- reduces friction
    
- increases compliance
    

You don’t challenge authority  
You **align beneath it**

---

