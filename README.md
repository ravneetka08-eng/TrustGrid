# TrustGrid
 The Future of Identity Security Starts Here:  **Secure humans. Secure AI agents. Trust every identity.**

An AI-first Identity and Access Management (IAM) platform built for organisations where humans and autonomous AI agents work together.

<br>

## What TrustGrid secures

### Human Identities
- Employees
- Administrators
- Customers
- Contractors
- Authentication: **Password + TOTP MFA**

### AI Agents
- Automation bots
- Reporting agents
- Integration services
- Authentication: **API Key + JWT**

### Service Accounts
- APIs
- Microservices
- Data pipelines
- Registered in the **Agent Registry** with scoped permissions

### Rogue Identities
- Unknown or unregistered agents
- Access blocked immediately
- Logged in the audit trail
- Flagged on the Security Dashboard


<br>

## Why agent identity matters — industry examples
1. Financial services

ATTACK SCENARIO — high risk

Rogue trading agent accesses the loan approval database
A compromised trading agent attempts to read the loan database — a resource outside its registered permissions. Without identity management, the database cannot distinguish it from a legitimate service call.
Without TrustGrid: Thousands of customer loan records exfiltrated undetected. Breach discovered weeks later in a regulatory audit.
With TrustGrid: Request blocked against allowed_resources. PERMISSION_VIOLATION logged. Admin alerted within seconds.

INSIDER THREAT — medium risk
Employee deploys an unsanctioned AI agent
A developer quietly deploys a personal automation agent using their credentials. It begins reading client portfolio data at machine speed — 10,000 records per minute.
Without TrustGrid: Looks like normal API usage. Nobody notices until a client complaint surfaces the exposure.
With TrustGrid: No registered agent_id returns 401. UNKNOWN_AGENT alert fires immediately. Security team investigates within minutes.

2. Healthcare

ATTACK SCENARIO — high risk
Scheduling agent queries full patient medical records
A compromised scheduling agent — which only needs names and appointment times — begins querying detailed patient medical histories across the entire system.
Without TrustGrid: Thousands of medical records exfiltrated. HIPAA violation. Multi-million dollar fine. Patient data on the dark web.
With TrustGrid: Medical records outside the agent's allowed_resources. Blocked, logged as PERMISSION_VIOLATION, auto-suspended after 3 violations. Resolved in under 5 minutes.

INSIDER THREAT — medium risk
Pharmacy agent authenticates from a new IP at 3am at 5× normal rate
The pharmacy dispensing agent connects from a new server IP at an unusual hour and begins processing prescriptions at 5× its normal rate — potentially a compromised agent being operated by an attacker.
Without TrustGrid: Activity goes undetected. Prescription records modified or exfiltrated before morning.
With TrustGrid: Risk engine scores 55 (new IP +25, rate spike +30). JWT invalidated. On-call admin alerted to re-verify before access restored.

3. Retail

ATTACK SCENARIO — high risk
Customer service agent issues unlimited refunds via stolen API key
A threat actor gains the customer service agent's API key and triggers thousands of refund requests in minutes, targeting high-value orders with no rate cap or per-session limit.
Without TrustGrid: $2.4 million in fraudulent refunds processed before a human notices the accounts anomaly the next morning.
With TrustGrid: Rate spike anomaly fires (50× normal in 10 min). Agent auto-suspended, key invalidated, ROGUE_AGENT_ALERT raised. Losses stopped within minutes.

OPERATIONAL SCENARIO — medium risk
Pricing agent accidentally writes to the customer payment database
A misconfigured update gives the pricing agent write access to the payment database. It begins logging price adjustments to the wrong table, corrupting payment records at scale.
Without TrustGrid: Corrupted payment records cause incorrect charges to thousands of customers. 3-day outage to debug the source.
With TrustGrid: Payment database not in allowed_resources. Every write blocked and logged. Misconfiguration caught on first attempt — before any data is corrupted.

<br>

##  Tech Stack

| Category | Technologies |
|----------|--------------|
| **Language** | Python 3.x |
| **Framework** | Flask, Flask-SQLAlchemy, Flask-Mail |
| **Authentication & Cryptography** | bcrypt, PyOTP, PyJWT, qrcode, secrets |
| **Database** | SQLite |
| **Frontend** | HTML, CSS, JavaScript, Chart.js |
| **Geolocation** | ip-api.com |
| **Testing & Security** | pytest, OWASP ZAP, Burp Suite Community Edition |
| **Development Tools** | VS Code, Git, GitHub, Postman |


<br>

## Future improvements

- Replace rule-based risk scoring with a trained ML model (e.g., Isolation Forest for anomaly detection)
- Certificate-based agent authentication using mTLS instead of API keys
- OAuth 2.0 / OpenID Connect SSO integration with Microsoft Entra ID or Keycloak
- Per-agent rate limiting to prevent volumetric abuse
- Real-time security alerts via webhooks or Slack integration
- Agent-to-agent trust verification for secure AI-to-AI communication
