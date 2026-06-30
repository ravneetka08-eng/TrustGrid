# NexusBank

This document defines the complete identity surface of NexusBank — every human role, every AI agent, every protected resource, and the access boundaries between them.

It is the foundational input for TrustGrid's authentication flows, RBAC permission map, agent registry, and audit event schema.

Any identity not defined here is not permitted to operate within the platform.

<br>

# Purpose of this document

Modern financial institutions operate a mixed workforce of human employees and autonomous AI agents. Both types of identity access sensitive systems, process confidential data, and make decisions that carry regulatory and financial consequences. Traditional IAM platforms were not designed for this model.

This document scopes TrustGrid's deployment at NexusBank — defining who exists, what they can access, what they are blocked from, and what governance rules apply.

Every table, every permission decorator, every audit event in the TrustGrid implementation traces back to a decision made in this document.

<br>

# Organisation Context

| Attribute | Value |
|----------|------|
| Organisation | NexusBank |
| Sector | Financial services |
| Customers | 84 million |
| Staff | 250,000 |
| AI agents | 8 registered |
| Jurisdictions | US, EU, UK |
| Regulations | DORA, GDPR, GLBA |
| IAM platform | TrustGrid v1.0 |

## Departments in scope
- Consumer banking
- Investment banking
- Asset and wealth management
- Fraud and financial crime
- Software engineering
- Call centre operations
- Compliance and legal
- IT security operations
- Credit and lending
- Data and analytics

<br>

# Protected Resources — Classified by Sensitivity

| Resource | Description | Sensitivity |
|----------|------------|--------------|
| Customer PII database | Names, addresses, national IDs, passports, tax identifiers | Critical |
| Transaction records | All customer payment and transfer history. Regulated under GLBA and GDPR | Critical |
| Loan approval database | Credit decisions, loan terms, risk scores, collateral records | Critical |
| Fraud detection system | Real-time fraud rules, alert thresholds, blocked account flags | Critical |
| Client portfolio data | Investment holdings, positions, advisory notes. Wealth management data | High |
| Compliance and audit records | Regulatory filings, internal audit logs, sanctions screening results | High |
| Market data feed | Real-time and historical market prices, indices, macroeconomic data | Medium |
| SEC and regulatory filings | Public filings accessed for research and due diligence (read-only) | Medium |
| Internal knowledge base | Policy documents, HR materials, internal procedures. Non-customer data | Medium |
| Code repository and CI/CD | Source code, pipelines, and deployment infrastructure (dev environments only) | Medium |
| Client deal database | Investment banking deal flow, M&A data, client mandates | High |
| HR and payroll records | Employee salaries, performance reviews, disciplinary records | Critical |

<br>

# Human Identity Catalogue — 6 Roles

## System Administrator
IT Security Operations

### Permitted
- TrustGrid admin dashboard  
- Agent registry — full CRUD  
- User and role management  
- All audit logs read  
- Threat alert management  

### Blocked from
- Customer PII database  
- Transaction records  
- Client portfolio data  
- Loan approval database  

---

## Investment Banker
Investment Banking

### Permitted
- Client deal database read/write  
- Market data feed read  
- SEC filings read  
- Presentation output write  

### Blocked from
- Customer PII database  
- Transaction records  
- Fraud detection system  
- Loan approval database  
- HR and payroll records  
- Client portfolio data  

---

## Wealth Adviser
Asset and Wealth Management

### Permitted
- Client portfolio data read  
- Market data feed read  
- Advisory notes write  
- Research reports read  

### Blocked from
- Customer PII database  
- Transaction records  
- Fraud detection system  
- Loan approval database  
- HR and payroll records  
- Code repository  
- Client deal database  

---

## Call Centre Agent
Call Centre Operations

### Permitted
- Customer account read  
- Transaction history read  
- Case management write  
- Policy knowledge base read  

### Blocked from
- Client portfolio data  
- Fraud detection system  
- Loan approval database  
- Compliance and audit records  
- HR and payroll records  
- Code repository  
- Client deal database  

---

## Software Engineer
Software Engineering

### Permitted
- Code repository read/write  
- CI/CD pipeline read/write  
- Dev environment full access  
- Internal knowledge base read  

### Blocked from
- Customer PII database  
- Transaction records  
- Client portfolio data  
- Fraud detection system  
- Loan approval database  
- HR and payroll records  
- Production database (direct)  
- Compliance and audit records  

---

## Compliance Officer
Compliance and Legal

### Permitted
- Compliance and audit records  
- Risk reports read  
- Audit log read  
- Transaction records read  
- Sanctions screening results  

### Blocked from
- Client portfolio data  
- Client deal database  
- HR and payroll records  
- Code repository  
- Fraud detection write

<br>

# AI Agent Identity Catalogue — 8 Registered Agents

---

## Deck Generation Agent

Generates investment banking presentation decks autonomously using deal data and market context. Work that previously took a team of analysts hours is completed in under a minute. Operates entirely within deal and market data — no customer contact.

**Owner role:** Investment banker  
**Department:** Investment banking  
**Status:** Active  

### Permitted resources
- Client deal database — read  
- Market data feed — read  
- SEC filings — read  
- Presentation output — write  

### Blocked from all others including
- Customer PII database  
- Transaction records  
- Fraud detection system  
- Loan approval database  
- Client portfolio data  
- HR and payroll records  
- Compliance and audit records  
- Code repository and CI/CD  
- Internal knowledge base  

---

## Fraud Detection Agent

Analyses the live transaction stream in real time to flag anomalous activity. Reduces false positive rates that reached as high as 95% under legacy rule-based systems. Raises alerts — never blocks accounts autonomously without human review.

**Owner role:** Compliance officer  
**Department:** Fraud and financial crime  
**Status:** Active  

### Permitted resources
- Transaction stream — read  
- Customer account status — read  
- Fraud alert queue — write  

### Blocked from all others including
- Customer PII database  
- Client portfolio data  
- Loan approval database  
- Compliance and audit records  
- Client deal database  
- HR and payroll records  
- Market data feed  
- Code repository and CI/CD  
- Internal knowledge base  

---

## Wealth Advisory Agent

Surfaces research, market context, and client-specific insights to wealth advisers during client interactions and periods of market volatility. Compresses adviser preparation time from hours to seconds. Does not write to client accounts or execute trades.

**Owner role:** Wealth adviser  
**Department:** Asset and wealth management  
**Status:** Active  

### Permitted resources
- Client portfolio data — read  
- Market research feed — read  
- Market data feed — read  
- Advisory notes — write  

### Blocked from all others including
- Customer PII database  
- Transaction records  
- Loan approval database  
- Fraud detection system  
- Compliance and audit records  
- Client deal database  
- HR and payroll records  
- Code repository and CI/CD  
- Call centre AI assistant  

---

## Call Centre AI Assistant

Provides call centre staff with instant answers to customer enquiries by querying policy documents and transaction histories. Reduces resolution time and human error on high-volume, unpredictable call types. Supports human agents — does not interact with customers directly.

**Owner role:** Call centre manager  
**Department:** Call centre operations  
**Status:** Active  

### Permitted resources
- Policy knowledge base — read  
- Transaction history — read  
- Customer account — read  
- Case notes — write  

### Blocked from all others including
- Customer PII database  
- Client portfolio data  
- Fraud detection system  
- Loan approval database  
- Compliance and audit records  
- Client deal database  
- HR and payroll records  
- Code repository and CI/CD  
- Market data feed  

---

## Code Testing Agent

Continuously analyses bank software and generates test cases for edge cases and component dependencies across engineering services. Operates exclusively in the development environment — zero access to production systems or customer data of any kind.

**Owner role:** Software engineer  
**Department:** Software engineering  
**Status:** Active  

### Permitted resources
- Code repository — read  
- Test suite — write  
- CI/CD pipeline — read  
- Dev environment — read/write  

### Blocked from all others including
- Customer PII database  
- Transaction records  
- Client portfolio data  
- Fraud detection system  
- Loan approval database  
- Compliance and audit records  
- HR and payroll records  
- Production database (direct)  
- Client deal database  

---

## Investment Research Agent

Automates multi-step investment research tasks — querying SEC filings, summarising regulatory documents, and generating structured research reports for analysts. Reads only public and licensed data sources. Cannot write to deal databases or client records.

**Owner role:** Investment banker  
**Department:** Investment banking  
**Status:** Active  

### Permitted resources
- SEC and regulatory filings — read  
- Market data feed — read  
- Research report output — write  

### Blocked from all others including
- Customer PII database  
- Transaction records  
- Client portfolio data  
- Fraud detection system  
- Loan approval database  
- Client deal database  
- HR and payroll records  
- Compliance and audit records  
- Code repository and CI/CD  

---

## Employee Productivity Agent

A firm-wide AI assistant available to all staff for document summarisation, email drafting, idea generation, and querying internal procedures. Operates solely on non-customer, non-financial internal data. Rolled out across all business lines.

**Owner role:** System administrator  
**Department:** All departments  
**Status:** Active  

### Permitted resources
- Internal knowledge base — read  
- Document generation — write  
- Email draft — write  

### Blocked from all others including
- Customer PII database  
- Transaction records  
- Client portfolio data  
- Fraud detection system  
- Loan approval database  
- Client deal database  
- HR and payroll records  
- Compliance and audit records  
- Code repository and CI/CD  

---

## Credit Card Upgrade Agent

Identifies customers eligible for credit card upgrades by analysing spending patterns and account behaviour, then triggers personalised outreach campaigns. Operates on aggregated spending signals — never accesses raw PII or transaction detail.

**Owner role:** Compliance officer  
**Department:** Consumer banking  
**Status:** Active  

### Permitted resources
- Customer account — read  
- Spending pattern signals — read  
- Outreach campaign — write  

### Blocked from all others including
- Customer PII database  
- Transaction records (raw)  
- Client portfolio data  
- Fraud detection system  
- Loan approval database  
- Client deal database  
- HR and payroll records  
- Compliance and audit records  
- Code repository and CI/CD

---

<br>

# Governance and Security Principles

- Every identity registered: No agent operates without a record in TrustGrid's agent registry. No human role exists outside the defined catalogue.
- Least privilege by default: Every identity receives the minimum access required for its defined purpose. Access not listed in this document is denied by default.
- Continuous trust evaluation: Authentication is not a one-time event. Risk is re-scored on every login and flagged for anomalous behaviour post-authentication.
- Human ownership of agents: Every AI agent has a named human owner accountable for its behaviour. Ownerless agents are not permitted to operate.
- Full audit trail: Every authentication, authorisation decision, and block is logged. Logs are append-only. No identity — human or agent — operates without a traceable record.
- Zero standing access for agents: Agent credentials are short-lived JWTs with a 30-minute TTL. No agent holds persistent standing access to any resource.

---

<br>

# Regulatory Alignment

- DORA (EU, 2025): Requires financial entities to maintain a comprehensive register of ICT third-party and internal digital service arrangements. TrustGrid's agent registry directly satisfies this obligation.
- GDPR: Customer PII and transaction records are classified Critical and blocked from all agents unless explicitly granted. Every access decision is logged with timestamp and actor identity.
- GLBA (US): Financial data access is scoped, logged, and traceable to a named identity. No agent accesses customer financial records without a registered permission.
- EU AI Act (2026): High-risk AI systems must maintain logs for traceability. TrustGrid's append-only audit log with 18 event types satisfies this requirement by design.



