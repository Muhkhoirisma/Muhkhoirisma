# Bug Bounty Portfolio

**Handle:** Muhkhoirisma

**Focus:** IDOR, Broken Access Control, API Security, Authorization Testing

---

# 📌 About Me

Security researcher with experience reporting security vulnerabilities through official Vulnerability Disclosure Programs (VDP) and Bug Bounty platforms.

My primary research areas include:

* Broken Access Control
* Insecure Direct Object Reference (IDOR)
* Authorization Testing
* API Security
* Business Logic Testing

---

# 🏆 Achievements

| # | Finding                                                   | Result                                                         |
| - | --------------------------------------------------------- | -------------------------------------------------------------- |
| 1 | **IDOR – Kredivo**                                        | ✅ Valid, accepted and rewarded                                 |
| 2 | **Unauthenticated Endpoint – Bali Provincial Government** | ✅ Official Certificate of Appreciation                         |
| 3 | **NASA Vulnerability Disclosure Program**                 | ✅ Security report submitted                                    |
| 4 | **Broken Access Control – Agoda (HackerOne)**             | ✅ Valid vulnerability (Duplicate of previously reported issue) |

---

# 🛠 Case Studies

## Case 1 — IDOR in Deprecated API Endpoint

**Target:** Kredivo

**Category:** IDOR / Broken Access Control

### Summary

Identified an authorization flaw within a legacy API endpoint that remained accessible after migration.

### Impact

Changing the object identifier allowed unauthorized access to another user's account information.

### Result

* Accepted
* Bounty awarded

---

## Case 2 — Unauthenticated Endpoint

**Target:** Bali Provincial Government

**Category:** Authentication Bypass

### Summary

A product import functionality could be accessed without authentication.

### Impact

Potential unauthorized manipulation of UMKM product data.

### Result

* Accepted
* Official appreciation certificate awarded

---

## Case 3 — Cross-Account Booking Information Disclosure

**Target:** Agoda (HackerOne)

**Category:** Broken Access Control / Missing Authorization

### Summary

During authorization testing using two researcher-controlled accounts, I identified that the booking status endpoint returned booking information based solely on a supplied **pollingToken** without validating ownership against the authenticated user session.

Replacing the polling token of Account A with the polling token belonging to Account B caused the application to return booking information associated with Account B while remaining authenticated as Account A.

The disclosed response included booking-related metadata such as:

* Booking ID
* Itinerary ID
* Booking Status
* Payment Session URL
* Self-Service Booking URL

Testing was performed exclusively using researcher-controlled accounts in accordance with the program policy.

### Result

**Status:** Duplicate

The HackerOne triage team confirmed that the vulnerability had already been reported under an earlier report (#3812532).

Although no bounty was awarded, the submission independently reproduced the same authorization flaw and demonstrated a valid security issue.

### Skills Demonstrated

* API Reconnaissance
* Authorization Testing
* Broken Access Control Assessment
* Cross-Account Access Testing
* Burp Suite Professional
* HTTP Request Analysis
* Vulnerability Documentation
* Responsible Disclosure

---

# 🧰 Tools

* Burp Suite Professional
* Burp Repeater
* Burp Proxy
* Dirsearch
* Google Chrome DevTools
* Manual API Testing

---

# 🎯 Current Research

Currently focused on identifying:

* Broken Access Control
* IDOR
* Authorization Logic Issues
* API Security Vulnerabilities
* Business Logic Flaws

through public and private bug bounty programs.

---

# 📬 Contact

Email:

**[sad306391@gmail.com](mailto:sad306391@gmail.com)**

---

# 📸 Supporting Evidence

* Kredivo Bounty Confirmation
* Bali Provincial Government Certificate
* HackerOne Report Status (Agoda – Duplicate)

Sensitive information has been redacted to comply with responsible disclosure policies.

---

# ⚖ Responsible Disclosure

All testing has been performed only against researcher-controlled accounts or within the scope of authorized vulnerability disclosure programs.

No third-party user data was intentionally accessed, modified, or retained.

Technical exploitation details and sensitive information have been intentionally omitted.
