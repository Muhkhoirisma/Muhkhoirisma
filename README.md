# 🛡 Bug Bounty & Security Research Portfolio

<p align="center">

**Security Researcher | API Security | Broken Access Control | IDOR | Authorization Testing**

</p>

---

# 👋 About Me

Hello, I'm **Muhkhoirisma**, an independent Security Researcher specializing in **manual application security testing**, with a primary focus on identifying authorization weaknesses and API security vulnerabilities.

I actively participate in Vulnerability Disclosure Programs (VDP) and Bug Bounty platforms, conducting responsible security research against authorized targets.

My research emphasizes understanding application logic rather than relying solely on automated tools, allowing me to identify complex authorization flaws and business logic vulnerabilities.

---

# 🎯 Research Focus

- Broken Access Control
- Insecure Direct Object Reference (IDOR)
- Authorization Testing
- API Security
- Business Logic Testing
- Authentication Analysis
- REST API Security
- Cross-Account Access Control

---

# 🔬 Research Methodology

My research follows a structured manual testing methodology consisting of:

1. Reconnaissance
2. Endpoint Enumeration
3. Authentication Analysis
4. Authorization Assessment
5. Cross-Account Validation
6. API Abuse Testing
7. Business Logic Analysis
8. Root Cause Analysis
9. Vulnerability Validation
10. Responsible Disclosure

I prioritize understanding how an application enforces authorization rather than relying on automated scanners.

---

# 🏆 Achievements

| # | Finding | Result |
|---|---------|--------|
| 1 | **IDOR – Kredivo** | ✅ Accepted & Rewarded |
| 2 | **Unauthenticated Endpoint – Bali Provincial Government** | ✅ Official Certificate of Appreciation |
| 3 | **NASA Vulnerability Disclosure Program** | ✅ Security Report Submitted |
| 4 | **Broken Access Control – Agoda (HackerOne)** | ✅ Valid Vulnerability (Duplicate) |
| 5 | **Broken Access Control / IDOR – NBA Identity (HackerOne)** | ✅ Valid Vulnerability (Duplicate) |

---

# 🛠 Case Studies

---

## Case 1 — IDOR in Deprecated API Endpoint

**Target:** Kredivo

**Category**

- IDOR
- Broken Access Control

### Summary

Identified an authorization flaw within a deprecated API endpoint that remained accessible after system migration.

### Impact

Manipulating the object identifier allowed unauthorized access to another user's account information.

### Result

- ✅ Accepted
- 💰 Bounty Awarded

---

## Case 2 — Unauthenticated Product Import Endpoint

**Target:** Bali Provincial Government

**Category**

Authentication Bypass

### Summary

Identified an administrative product import functionality that could be accessed without authentication.

### Impact

Potential unauthorized modification of public UMKM product data.

### Result

- ✅ Accepted
- 📜 Official Certificate of Appreciation

---

## Case 3 — Cross-Account Booking Information Disclosure

**Target:** Agoda (HackerOne)

**Category**

- Broken Access Control
- Missing Authorization

### Summary

During authorization testing using two researcher-controlled accounts, I discovered that the booking status endpoint relied solely on a supplied **pollingToken** without verifying ownership against the authenticated session.

Replacing the polling token belonging to Account A with one belonging to Account B caused the application to disclose booking information associated with Account B.

### Information Exposed

- Booking ID
- Itinerary ID
- Booking Status
- Payment Session URL
- Self-Service Booking URL

Testing was performed exclusively using researcher-controlled accounts.

### Result

**Status:** Duplicate

The HackerOne triage team confirmed that the vulnerability had already been reported under an earlier report (**#3812532**).

Although no bounty was awarded, the submission independently reproduced the authorization flaw.

---

## Case 4 — Cross-Account Profile Metadata Disclosure

**Target:** NBA Identity (HackerOne)

**Category**

- Broken Access Control
- IDOR
- Missing Authorization

### Summary

During authorization testing of the NBA Identity platform, I identified an authorization weakness where profile metadata belonging to another user could be accessed by manipulating the user identifier (UUID) supplied to the API.

The endpoint returned profile metadata without verifying that the requested UUID belonged to the authenticated user.

Testing was performed exclusively using researcher-controlled accounts.

### Impact

An authenticated attacker could retrieve another user's profile metadata due to insufficient object-level authorization checks.

The issue demonstrated a classic Broken Access Control vulnerability affecting user profile resources.

### Result

**Status:** Duplicate

The HackerOne triage team confirmed that the vulnerability had already been reported under an earlier report (**#3749507**).

Although no bounty was awarded, the report independently reproduced the same authorization weakness, and the root cause was confirmed as insufficient authorization checks.

---

# 💼 Technical Skills

## Security Testing

- API Security Testing
- Authorization Testing
- Broken Access Control Assessment
- IDOR Discovery
- Business Logic Analysis
- Authentication Analysis
- REST API Testing
- Manual Penetration Testing

## Security Research

- Endpoint Enumeration
- HTTP Protocol Analysis
- API Reconnaissance
- Cross-Account Testing
- Root Cause Analysis
- Vulnerability Validation
- Responsible Disclosure

---

# 🧰 Tools

- Burp Suite Professional
- Burp Proxy
- Burp Repeater
- Burp Intruder
- Google Chrome DevTools
- Dirsearch
- ffuf
- Postman
- curl
- Manual API Testing

---

# 📈 Current Research

Currently researching:

- Broken Access Control
- IDOR
- Authorization Logic Flaws
- API Security
- Business Logic Vulnerabilities
- Object-Level Authorization
- Session Management
- Access Control Validation

through public and private Vulnerability Disclosure Programs.

---

# 📸 Supporting Evidence

- ✅ Kredivo Bounty Confirmation
- ✅ Bali Provincial Government Certificate
- ✅ HackerOne Report Status (Agoda – Duplicate)
- ✅ HackerOne Report Status (NBA Identity – Duplicate)

Sensitive information has been redacted in accordance with responsible disclosure practices.

---

# ⚖ Responsible Disclosure

All research has been performed only within the scope of authorized Vulnerability Disclosure Programs or Bug Bounty Programs.

Testing has been conducted exclusively using researcher-controlled accounts.

No third-party user data was intentionally accessed, modified, retained, or disclosed.

Technical exploitation details have been intentionally omitted to comply with responsible disclosure policies.

---

# 📚 Research Philosophy

I believe effective security research is built on curiosity, patience, and a deep understanding of application behavior.

My objective is not only to discover vulnerabilities but also to understand their root causes, validate their real-world impact, and contribute to improving application security through responsible disclosure.

---

# 📬 Contact

📧 **Email**

**sad306391@gmail.com**

---

> *"Every rejected report is feedback. Every duplicate is validation. Every accepted report is the result of continuous learning."*
