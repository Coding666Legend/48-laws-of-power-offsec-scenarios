## **Law 1 — Never Outshine the Master**

Interpretation (offensive context):  
Maintain **perceived inferiority to authority** to avoid scrutiny, bypass ego defenses, and gain cooperation.

---

# 🎯 Attack Scenario — _Helpdesk Credential Reset via Subordinate Persona_

A low-privilege attacker impersonates a **junior employee** to manipulate IT support into resetting credentials for a higher-value account.

**Persona:**

> _Anastasia Ivanova_, 20 y/o intern (Finance Dept)

---

# 🔴 Red Team Objective

- Gain **initial access credentials** without triggering suspicion
    
- Exploit **authority bias + ego preservation**
    

---

# 🖥️ Lab Setup (lightweight, within 16GB constraint)

### VMs:

- **Kali (Attacker)** — 3GB RAM / 2 vCPU
    
- **Ubuntu (Victim – Helpdesk simulation)** — 2GB RAM / 1 vCPU
    

### Network:

- **Host-only network**
    
- No internet dependency required
    

### Optional:

- Simple internal “directory” file (CSV) to simulate employee data
    

---

# ⚙️ Operator Workflow

## Phase 1 — Recon (Human Layer)

Goal: Identify **authority structure**

### Action:

Create a small dataset:

```
Name, Role, Email
Elena Petrova, IT Support, elena.p@corp.local
David Clarke, Finance Manager, d.clarke@corp.local
```

👉 You now know:

- Who has authority (IT)
    
- Who is valuable (Manager)
    

---

## Phase 2 — Persona Construction

You deliberately **lower your perceived status**:

```
Name: Anastasia Ivanova
Role: Finance Intern
Tone: Hesitant, respectful
Objective: Request password reset "on behalf of manager"
```

Key tactic:

> You never sound smarter than the helpdesk

---

## Phase 3 — Pretext Execution (Core Exploit)

### Script:

> “Hi… sorry to bother you… I’m new here…  
> Mr. Clarke asked me to get his account working, he’s in a meeting… I might have messed something up…”

This triggers:

- Authority bias (manager mentioned)
    
- Sympathy (junior mistake)
    
- Ego (helpdesk feels superior)
    

---

## Phase 4 — Delivery Simulation

### Method:

Local simulation via email (safe lab)

---

## 🛠️ Tooling + Commands

### Option 1 — Manual SMTP (cleanest for understanding)

On Kali:

```bash
sudo apt install swaks -y
```

Send crafted email:

```bash
swaks --to elena.p@corp.local \
--from anastasia.i@corp.local \
--server 192.168.56.102 \
--data "Subject: Urgent Help Needed

Hi Elena,

Sorry if this is silly, I just joined and I think I locked Mr. Clarke's account while trying to access a file he asked for.

He’s currently in a meeting and asked me to get it sorted quickly.

Could you please reset it or guide me?

Thanks,
Anastasia"
```

---

### Option 2 — SET (if you want automation later)

```bash
setoolkit
```

Navigate:

```
1) Social Engineering Attacks
2) Mass Mailer Attack
```

(But manual is better for learning control)

---

## Phase 5 — Expected Result

Helpdesk responds with:

- reset link
    
- temporary password
    
- verification bypass
    

👉 That is your **initial access vector**

---

# 🧠 Social Engineering Mapping (Hadnagy)

Relevant concepts:

- **Ego exploitation** → You appear less competent
    
- **Authority transfer** → Mention of manager
    
- **Pretexting** → Fully constructed believable scenario
    

Critical principle:

> People help those who make them feel competent

---

# 🛡️ Detection & Defensive Insight

What should flag this:

- Password reset requests **via third party**
    
- Lack of identity verification
    
- Urgency tied to authority
    

Mitigation:

- Enforce **direct user verification**
    
- Helpdesk script hardening:
    
    - “We cannot reset without speaking to account owner”
        

---

# 📄 Report Artifact (what you document)

### Title:

> Helpdesk Credential Reset via Subordinate Persona Exploitation

### Include:

- Attack narrative
    
- Pretext script
    
- Email artifact
    
- Psychological triggers used
    
- Impact:
    
    - Unauthorized account access
        
- Recommendation:
    
    - Multi-factor identity verification
        

---

# ⚠️ Operator Insight (important)

If you acted as:

- confident
    
- technical
    
- assertive
    

→ You would trigger suspicion

Your success depends on:

> Controlled incompetence

---
