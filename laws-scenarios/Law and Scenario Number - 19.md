## **Law 19 — Know Who You’re Dealing With**

Interpretation (offensive context):  
A generic pretext fails against diverse personalities. You must **profile the target (role, behavior, tolerance, incentives)** and tailor the attack accordingly. Wrong profile → detection.

---

# 🎯 Attack Scenario — _Personality-Tailored Social Engineering (Adaptive Pretexting)_

You analyze two different users and deploy **distinct attack strategies** based on their profiles.

**Personas (targets):**

- _Oliver Grant_ — Senior Finance Analyst (methodical, cautious)
    
- _Lily Novak_ — HR Intern (responsive, less experienced)
    

**Attacker Persona:**

> _Mila Petrova_, 20 y/o Internal Ops Intern

---

# 🔴 Red Team Objective

- Increase success by:
    
    - **customizing attack per target**
        
- Avoid:
    
    - one-size-fits-all phishing (high failure rate)
        

---

# 🖥️ Lab Setup

### VMs:

- **Kali (Attacker)** — 3GB
    
- **Ubuntu Victim 1 (Oliver)** — 2GB
    
- **Ubuntu Victim 2 (Lily)** — 2GB
    

### Network:

- Host-only
    

---

# ⚙️ Operator Workflow

## Phase 1 — Target Profiling

Simulate dataset:

```id="y7v9c2"
Name, Role, Behavior
Oliver Grant, Finance Analyst, cautious
Lily Novak, HR Intern, responsive
```

---

## Phase 2 — Strategy Selection

### Target 1: Oliver (Cautious)

Bad approach:

- vague email → ignored
    

Correct approach:

- **detailed, structured, formal**
    

---

### Target 2: Lily (Responsive)

Bad approach:

- long explanation → overthinking
    

Correct approach:

- **simple, quick task**
    

---

## Phase 3 — Attack Execution

### 🎯 Attack A — Cautious Target (Oliver)

```bash
swaks --to oliver@corp.local \
--from mila.p@corp.local \
--server 192.168.56.101 \
--data "Subject: Finance system validation

Hi Oliver,

We are validating access logs for the finance portal. Please verify your access via the internal link below:

http://192.168.56.101:8080

Regards,
Mila"
```

👉 Structured  
👉 Formal  
👉 Aligned with role

---

### 🎯 Attack B — Responsive Target (Lily)

```bash
swaks --to lily@corp.local \
--from mila.p@corp.local \
--server 192.168.56.101 \
--data "Subject: Quick check

Hi,

Can you quickly confirm access here?

http://192.168.56.101:8080"
```

👉 Short  
👉 Low friction

---

## Phase 4 — Payload

```bash
php -S 0.0.0.0:8080
```

Credential capture as before.

---

## Phase 5 — Expected Result

- Oliver:
    
    - responds to structured authority
        
- Lily:
    
    - responds to simplicity
        

👉 Same payload  
👉 Different delivery = higher success

---

# 🛠️ Tooling + Commands

### Profiling:

```bash
cat employees.csv
```

---

### Filtering:

```bash
grep -i "intern\|analyst" employees.csv
```

---

### Delivery:

```bash
swaks --to target@corp.local --from mila.p@corp.local
```

---

### Hosting:

```bash
php -S 0.0.0.0:8080
```

---

# 🧠 Social Engineering Mapping (Hadnagy)

Relevant concepts:

- **Target profiling**
    
- **Behavioral adaptation**
    
- **Pretext customization**
    

Key principle:

> The attack must match the person, not the other way around

---

# 🛡️ Detection & Defensive Insight

Indicators:

- role-specific phishing patterns
    
- tailored messaging based on job function
    

Mitigation:

- train:
    
    - all roles, not just technical teams
        
- simulate:
    
    - targeted phishing scenarios
        
- monitor:
    
    - unusual but role-consistent requests
        

---

# 📄 Report Artifact

### Title:

> Adaptive Social Engineering via Target Profiling

### Include:

- two target profiles
    
- two distinct attack approaches
    
- comparison:
    
    - why each worked differently
        
- captured credentials
    
- impact:
    
    - increased success via personalization
        

---

# ⚠️ Operator Insight

Generic attack:

- low success
    
- high noise
    

Tailored attack:

- high success
    
- low visibility
    

You’re not attacking “a user”  
You’re attacking **a specific human profile**

---

