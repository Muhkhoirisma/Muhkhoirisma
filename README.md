# Muhkhoirisma

**Offensive Security Researcher | API Authorization Testing | Broken Access Control | IDOR | Business Logic Abuse**

Hello, I'm **Muhkhoirisma**, an independent security researcher focused on **manual application and API security testing**, especially around **authorization weaknesses**, **broken access control**, **IDOR**, **cross-account access issues**, and **business logic flaws**.

My research emphasizes understanding how applications enforce authorization, rather than relying solely on automated scanners. I conduct responsible security research against authorized targets through Vulnerability Disclosure Programs and Bug Bounty platforms.

---

## Core Focus

- API Security Testing
- Broken Access Control Assessment
- Insecure Direct Object Reference / IDOR Discovery
- Object-Level Authorization Testing
- Function-Level Authorization Testing
- Cross-Account Validation
- Authentication Flow Analysis
- Business Logic Abuse Testing
- Endpoint Enumeration and API Reconnaissance
- Root Cause Analysis
- Security Misconfiguration Assessment
- Information Disclosure Testing
- Responsible Disclosure

---

## Methodology

My testing approach follows a structured manual methodology:

1. **Reconnaissance**  
   Identify application surface, technologies, endpoints, authentication mechanisms, and possible trust boundaries.

2. **Endpoint Enumeration**  
   Map active, hidden, legacy, and deprecated API endpoints where possible within authorized scope.

3. **Authentication Analysis**  
   Understand login flows, session handling, token usage, and identity boundaries.

4. **Authorization Assessment**  
   Test whether the application correctly enforces permissions for actions and resources.

5. **Cross-Account Validation**  
   Use controlled accounts to validate horizontal privilege escalation, object-level authorization failures, and data isolation issues.

6. **Business Logic Analysis**  
   Examine workflows, state transitions, pricing/discount logic, approval flows, and abuse opportunities that scanners usually miss.

7. **Root Cause Analysis**  
   Explain why the vulnerability exists, not only how it was found.

8. **Impact Validation**  
   Assess realistic security impact without accessing unauthorized third-party data.

9. **Responsible Disclosure**  
   Report findings clearly, ethically, and within program rules.

---

## Selected Research Outcomes

| # | Finding | Platform / Target | Result |
|---|---|---|---|
| 1 | IDOR / Broken Access Control | Kredivo | Accepted & Rewarded |
| 2 | Unauthenticated Administrative Functionality | Bali Provincial Government | Official Certificate of Appreciation |
| 3 | Security Research Submission | NASA Vulnerability Disclosure Program | Report Submitted |
| 4 | Broken Access Control / Missing Authorization | Agoda via HackerOne | Valid Vulnerability, Duplicate |
| 5 | Broken Access Control / IDOR | NBA Identity via HackerOne | Valid Vulnerability, Duplicate |
| 6 | Exposed Go pprof Debug Endpoint | Supra Security | Reported, Remediation Observed, Pending Triage |

> Note: Duplicate submissions still represent independent reproduction of confirmed authorization weaknesses. Where applicable, technical details are sanitized to comply with responsible disclosure policies.

---

## Case Studies

Detailed write-ups are available in the [`case-studies/`](./case-studies/) directory.

- [Kredivo — IDOR / Broken Access Control on Deprecated API Endpoint](./case-studies/kredivo-idor-broken-access-control.md)
- [Agoda — Missing Authorization on Booking Status Endpoint](./case-studies/agoda-missing-authorization.md)
- [Bali Provincial Government — Unauthenticated Administrative Functionality](./case-studies/bali-unauthenticated-admin-functionality.md)
- [NBA Identity — UUID-Based Broken Access Control](./case-studies/nba-identity-idor.md)
- [Supra — Exposed Go pprof Debug Endpoint](./case-studies/supra-exposed-pprof.md)

---

## Current Learning Track

I am actively expanding my research into more enterprise-relevant authorization and identity topics, including:

- OAuth 2.0 and OpenID Connect fundamentals
- JWT validation weaknesses
- Session management and token lifecycle issues
- Multi-tenant access control testing
- Horizontal vs vertical privilege escalation patterns
- Deprecated endpoint risk after system migration
- API gateway and microservice authorization boundaries
- Cloud-native API attack surfaces
- MITRE ATT&CK-informed application security testing

This learning track is intended to strengthen my ability to move from vulnerability discovery toward broader offensive security assessment thinking.

---

## Tools and Techniques

- Burp Suite Professional
- Burp Proxy / Repeater / Intruder
- Chrome DevTools
- Postman
- curl
- ffuf
- Dirsearch
- Manual HTTP/API testing
- Controlled account comparison testing
- Endpoint enumeration
- Request/response diffing
- Authorization boundary mapping

---

## Responsible Disclosure Statement

All research mentioned here was conducted only within the scope of authorized Vulnerability Disclosure Programs or Bug Bounty Programs.

Where account-based testing was required, testing was performed exclusively using researcher-controlled accounts. No third-party user data was intentionally accessed, modified, retained, or disclosed.

Sensitive technical details have been omitted or sanitized in accordance with responsible disclosure practices.

---
> “Every rejected report is feedback. Every duplicate is validation. Every accepted report is the result of continuous learning.”
