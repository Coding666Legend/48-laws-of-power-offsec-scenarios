## **Law 22 — Use the Surrender Tactic**

Interpretation (offensive context):  
When facing resistance or suspicion, **do not push harder**. Instead, **withdraw, concede, or appear to abandon the attempt**, then re-engage from a more advantageous position.

---

# 🎯 Attack Scenario — _Suspicion Trigger → Strategic Withdrawal → Clean Re-Entry_

Your initial attempt raises mild suspicion. Instead of escalating, you **de-escalate**, reset trust, and return later with a different angle.

**Personas:**

- Phase 1: _Natalie Brooks_ — HR Intern
    
- Phase 2: _Irina Sokolova_ — IT Support Assistant
    

---

# 🔴 Red Team Objective

- Avoid:
    
    - detection escalation
        
    - user reporting
        
- Recover:
    
    - compromised trust channel
        
- Achieve:
    
    - successful re-entry via alternate path
        

---

# 🖥️ Lab Setup

### VMs:

- **Kali (Attacker)** — 3GB
    
- **Ubuntu Victim** — 2GB
    

### Network:

- Host-only
    

---

# ⚙️ Operator Workflow

## Phase 1 — Initial Attempt (Trigger Suspicion)

```bash
swaks --to target@corp.local \
--from natalie.b@corp.local \
--server 192.168.56.101 \
--data "Subject: Policy update

Hi,

Please review the updated HR policy:

http://192.168.56.101:8080"
```

---

## Phase 2 — Resistance Detection

Simulated signals:

- no click
    
- delayed response
    
- user questions legitimacy
    

👉 This is a **red flag**

---

## Phase 3 — Strategic Surrender

Instead of pushing, you **withdraw cleanly**:

```bash
swaks --to target@corp.local \
--from natalie.b@corp.local \
--server 192.168.56.101 \
--data "Subject: Disregard

Hi,

Please ignore the previous message—sent in error.

Apologies."
```

👉 Effects:

- removes pressure
    
- lowers suspicion
    
- resets interaction
    

---

## Phase 4 — Cooling Period

Delay interaction (conceptual):

- hours / days
    

👉 Allows:

- memory fade
    
- trust recovery
    

---

## Phase 5 — Re-Entry (New Vector)

Switch identity + context:

```bash
swaks --to target@corp.local \
--from irina.s@corp.local \
--server 192.168.56.101 \
--data "Subject: Access issue

Hi,

We detected an issue with your account access. Please verify here:

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

- forgot initial suspicion
    
- sees new context
    
- interacts normally
    

👉 Surrender → Reset → Success

---

# 🛠️ Tooling + Commands

### Delivery:

```bash
swaks --to target@corp.local --from natalie.b@corp.local
```

```bash
swaks --to target@corp.local --from irina.s@corp.local
```

---

### Hosting:

```bash
php -S 0.0.0.0:8080
```

---

### Timing simulation:

```bash
sleep 60
```

---

# 🧠 Social Engineering Mapping (Hadnagy)

Relevant concepts:

- **Pressure removal** reduces resistance
    
- **Trust reset via apology**
    
- **Reframing attack context**
    

Key principle:

> Retreat is not failure—it’s repositioning

---

# 🛡️ Detection & Defensive Insight

Indicators:

- “ignore previous message” followed by new contact
    
- multiple identities targeting same user
    
- context switching
    

Mitigation:

- correlate:
    
    - prior suspicious interactions
        
- user training:
    
    - “A reset message doesn’t validate sender”
        
- track:
    
    - repeated targeting patterns
        

---

# 📄 Report Artifact

### Title:

> Social Engineering via Strategic Withdrawal and Re-Engagement

### Include:

- initial failed attempt
    
- surrender message
    
- re-entry attempt
    
- analysis:
    
    - how surrender reduced suspicion
        
- impact:
    
    - successful compromise after reset
        

---

# ⚠️ Operator Insight

Most attackers:

- double down after failure
    

That increases:

- suspicion
    
- detection
    

Real operators:

- disengage
    
- reset
    
- return clean
    

You don’t fight resistance  
You **remove it**

---

