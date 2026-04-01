## **Law 36 — Disdain Things You Cannot Have**

Interpretation (offensive context):  
Do not force access against **hardened or resistant targets**. Persisting increases detection risk. Recognize when a path is **high-cost / low-yield** and **pivot to a softer vector or adjacent target**.

---

# 🎯 Attack Scenario — _Abandon Hard Target → Pivot to Adjacent Low-Resistance Entry_

You attempt a high-value target (HVT). Signals indicate resistance. You **stop**, then **pivot to a nearby, weaker node** (e.g., assistant) to achieve the same objective indirectly.

**Primary Target (resistant):**

> _Edward Hastings_ — Finance Director

**Pivot Target (adjacent, softer):**

> _Lucy Bennett_, 20 y/o Executive Assistant

**Attacker Persona:**

> _Irina Volnova_, 20 y/o Ops Intern

---

# 🔴 Red Team Objective

- Avoid:
    
    - escalating suspicion on HVT
        
- Achieve:
    
    - **indirect access via adjacent user**
        
- Maintain:
    
    - low noise / low exposure
        

---

# 🖥️ Lab Setup

### VMs:

- **Kali (Attacker)** — 3GB
    
- **Ubuntu Victim 1 (HVT)** — 2GB
    
- **Ubuntu Victim 2 (Assistant)** — 2GB
    

### Network:

- Host-only
    

---

# ⚙️ Operator Workflow

## Phase 1 — Initial Attempt on HVT

```bash
swaks --to edward@corp.local \
--from irina.v@corp.local \
--server 192.168.56.101 \
--data "Subject: Access confirmation

Hi,

Please confirm your access:

http://192.168.56.101:8080"
```

---

## Phase 2 — Resistance Detection

Signals:

- no click
    
- delayed/guarded response
    
- verification request
    

👉 Interpretation:

- target is **highly cautious**
    

---

## Phase 3 — Strategic Abandonment

You **do not retry**  
You **do not escalate**

👉 You disengage completely from HVT

---

## Phase 4 — Identify Adjacent Target

Simulate relationship mapping:

```bash
cat employees.csv | grep -i "assistant"
```

```text
Lucy Bennett — Executive Assistant
```

👉 Likely:

- handles emails
    
- interacts with HVT workflows
    
- lower security awareness
    

---

## Phase 5 — Pivot Attack (Assistant)

```bash
swaks --to lucy@corp.local \
--from irina.v@corp.local \
--server 192.168.56.101 \
--data "Subject: Document for Edward

Hi,

Could you review this before forwarding to Edward?

http://192.168.56.101:8080"
```

👉 Delegation pretext  
👉 Lower resistance

---

## Phase 6 — Payload

```bash
php -S 0.0.0.0:8080
```

---

## Phase 7 — Execution

Assistant:

- trusts task
    
- interacts with link
    
- submits credentials
    

👉 Indirect access achieved

---

# 🛠️ Tooling + Commands

### Target mapping:

```bash
cat employees.csv
grep -i "assistant" employees.csv
```

---

### Delivery:

```bash
swaks --to lucy@corp.local --from irina.v@corp.local
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

# 🧠 Social Engineering Mapping (Hadnagy)

Relevant concepts:

- **Target selection adjustment**
    
- **Indirect exploitation**
    
- **Human attack surface mapping**
    

Key principle:

> If the front door is locked, don’t break it—use another entrance

---

# 🛡️ Detection & Defensive Insight

Indicators:

- targeting shifts:
    
    - from executives → assistants
        
- indirect access attempts
    
- delegation-based phishing
    

Mitigation:

- train:
    
    - assistants as **high-risk roles**
        
- enforce:
    
    - verification for delegated actions
        
- monitor:
    
    - unusual access patterns via support roles
        

---

# 📄 Report Artifact

### Title:

> Indirect Compromise via Strategic Target Abandonment and Pivoting

### Include:

- initial failed attempt
    
- pivot rationale
    
- assistant-targeted attack
    
- credential capture
    
- analysis:
    
    - why pivot succeeded
        
- impact:
    
    - indirect access to high-value workflows
        

---

# ⚠️ Operator Insight

Forcing access:

- increases risk
    
- decreases success
    

Abandoning strategically:

- preserves stealth
    
- opens better paths
    

You don’t win by persistence  
You win by **selection**

---

