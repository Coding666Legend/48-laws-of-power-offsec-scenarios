## **Law 43 — Work on the Hearts and Minds of Others**

Interpretation (offensive context):  
Move beyond surface-level tricks. Build **emotional rapport + cognitive alignment** so the target **wants to cooperate**. This enables deeper, repeated interactions with minimal resistance.

---

# 🎯 Attack Scenario — _Rapport-Driven Multi-Stage Engagement (Trust → Compliance → Access)_

You establish a **human connection first**, then gradually transition into operational requests. The user cooperates because of **relationship, not pressure**.

**Persona:**

> _Elena Sokolova_, 20 y/o New Operations Intern

**Target:**

> _Rahul Sharma_ — Senior Analyst

---

# 🔴 Red Team Objective

- Build:
    
    - trust + familiarity
        
- Enable:
    
    - repeated interaction channel
        
- Achieve:
    
    - eventual credential capture or intel extraction
        

---

# 🖥️ Lab Setup

### VMs:

- **Kali (Attacker)** — 3GB
    
- **Ubuntu Victim** — 2GB
    

### Network:

- Host-only
    

---

# ⚙️ Operator Workflow

## Phase 1 — Human Entry (No Technical Ask)

Initial message:

```bash
swaks --to rahul@corp.local \
--from elena.s@corp.local \
--server 192.168.56.101 \
--data "Subject: Quick intro

Hi Rahul,

I just joined the ops team—still getting familiar with how things work here. Hope it’s okay if I reach out occasionally."
```

👉 No objective  
👉 Only relationship building

---

## Phase 2 — Light Interaction (Familiarity)

Follow-up:

> “I noticed you work with the finance reports—do you usually access them through the main portal?”

👉 Extract:

- workflow
    
- system usage
    

---

## Phase 3 — Emotional Alignment

You mirror tone:

> “Got it, thanks—that helps a lot. Still figuring things out 😅”

👉 Effects:

- reduces distance
    
- builds comfort
    

---

## Phase 4 — Transition to Operational Request

```bash
swaks --to rahul@corp.local \
--from elena.s@corp.local \
--server 192.168.56.101 \
--data "Subject: Quick check

Hey,

I think I’m using the wrong page—does this look right?

http://192.168.56.101:8080"
```

👉 Not a command  
👉 Not a threat  
👉 A continuation of relationship

---

## Phase 5 — Payload

```bash
php -S 0.0.0.0:8080
```

---

## Phase 6 — Execution

Target:

- trusts sender
    
- wants to help
    
- interacts with link
    
- submits credentials
    

👉 Trust → compliance

---

# 🛠️ Tooling + Commands

### Communication:

```bash
swaks --to rahul@corp.local --from elena.s@corp.local
```

---

### Hosting:

```bash
php -S 0.0.0.0:8080
```

---

### Logging:

```php
file_put_contents("creds.txt", ...)
```

---

### Intel tracking:

```bash
nano notes.txt
```

---

# 🧠 Social Engineering Mapping (Hadnagy)

Relevant concepts:

- **Rapport building**
    
- **Elicitation over time**
    
- **Emotional manipulation (subtle)**
    

Key principle:

> People help those they like and trust

---

# 🛡️ Detection & Defensive Insight

Indicators:

- gradual relationship-building messages
    
- informal communication leading to requests
    
- new employees asking repeated questions
    

Mitigation:

- train users:
    
    - “Familiarity ≠ legitimacy”
        
- enforce:
    
    - verification even in casual interactions
        
- monitor:
    
    - unusual conversation patterns
        

---

# 📄 Report Artifact

### Title:

> Credential Harvest via Rapport-Based Social Engineering and Emotional Alignment

### Include:

- multi-stage conversation
    
- trust-building steps
    
- payload
    
- credential capture
    
- analysis:
    
    - how emotional trust enabled compromise
        
- impact:
    
    - high-confidence attack
        

---

# ⚠️ Operator Insight

Technical attacks:

- exploit systems
    

Advanced social engineering:

- exploits **relationships**
    

You’re not forcing access  
You’re **being invited in**

---

