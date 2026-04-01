## **Law 10 — Infection: Avoid the Unhappy and Unlucky**

Interpretation (offensive context):  
Not all targets are equal. Some users introduce **risk, noise, and detection probability**. Effective operators **select targets strategically** to maximize success and minimize exposure.

---

# 🎯 Attack Scenario — _Target Filtering for Low-Resistance Compromise_

Instead of attacking everyone, you **profile and select only high-probability, low-risk targets**.

**Persona (used later):**

> _Emily Dawson_, 20 y/o Admin Intern

---

# 🔴 Red Team Objective

- Increase:
    
    - success rate
        
    - stealth
        
- Decrease:
    
    - detection
        
    - reporting likelihood
        

---

# 🖥️ Lab Setup

### VMs:

- **Kali (Attacker)** — 3GB
    
- **Ubuntu Victim Pool (2 users simulated)** — 2GB each
    

### Network:

- Host-only
    

---

# ⚙️ Operator Workflow

## Phase 1 — Define “Bad Targets”

Avoid users who are:

- security-aware (IT, SOC)
    
- frustrated / suspicious (recent incidents)
    
- high authority (verify everything)
    
- technically skilled
    

👉 These increase:

- detection probability
    
- reporting likelihood
    

---

## Phase 2 — Define “Good Targets”

Select users who are:

- new employees
    
- interns
    
- non-technical roles
    
- overloaded with tasks
    

👉 These reduce:

- scrutiny
    
- resistance
    

---

## Phase 3 — Simulated Target Dataset

```id="0y7g8k"
Name, Role, Risk Level
John Miller, IT Admin, HIGH
Sophia Reed, HR Intern, LOW
Daniel Scott, Security Analyst, HIGH
Lucy Brown, Finance Assistant, LOW
```

👉 Only attack:

- Sophia Reed
    
- Lucy Brown
    

---

## Phase 4 — Pre-Attack Profiling (OSINT-style in lab)

Even in lab, simulate logic:

- Role → determines access
    
- Experience → determines awareness
    
- Behavior → determines susceptibility
    

---

## 🛠️ Tooling + Commands

### 1. Basic Enumeration Simulation

```bash
cat employees.csv
```

---

### 2. (Optional realistic approach)

Use:

```bash
theHarvester -d corp.local -l 50
```

👉 In real environments:

- gather employee emails
    
- infer roles
    

---

### 3. Filtering Targets

```bash
grep -i "intern\|assistant" employees.csv
```

👉 Extract low-risk targets

---

## Phase 5 — Attack Only Selected Targets

Example:

```bash
swaks --to sophia@corp.local \
--from emily.d@corp.local \
--server 192.168.56.101 \
--data "Subject: Quick task

Can you review this?

http://192.168.56.101:8080"
```

👉 No mass attack  
👉 Precision targeting

---

## Phase 6 — Expected Result

- Higher success rate
    
- Lower detection probability
    
- Cleaner operation
    

👉 Quality > quantity

---

# 🧠 Social Engineering Mapping (Hadnagy)

Relevant concepts:

- **Target profiling**
    
- **Human vulnerability assessment**
    
- **Pre-attack intelligence gathering**
    

Key principle:

> The right target is more important than the right payload

---

# 🛡️ Detection & Defensive Insight

Indicators:

- repeated targeting of:
    
    - interns
        
    - non-technical staff
        
- role-based attack patterns
    

Mitigation:

- train:
    
    - vulnerable groups (interns, HR, finance)
        
- simulate phishing across:
    
    - all departments
        
- monitor:
    
    - role-specific attack trends
        

---

# 📄 Report Artifact

### Title:

> Target Selection Optimization for Social Engineering Attacks

### Include:

- target classification model
    
- risk-based filtering logic
    
- attack comparison:
    
    - random vs targeted
        
- analysis:
    
    - why certain roles are more vulnerable
        
- impact:
    
    - improved success with reduced noise
        

---

# ⚠️ Operator Insight

Amateurs:

- attack everyone
    

Operators:

- attack **specific people for specific outcomes**
    

Bad target → failed operation  
Good target → effortless compromise

---

