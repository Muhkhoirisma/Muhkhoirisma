# Case Study: IDOR / Broken Access Control on Deprecated API Endpoint

**Target:** Kredivo  
**Platform:** Vulnerability Disclosure Program / Bug Bounty  
**Category:** IDOR, Broken Access Control  
**Result:** Accepted & Rewarded  
**Testing Mode:** Authorized manual security testing  

---

## Summary

During authorized manual API testing, I identified an authorization flaw on a deprecated endpoint that remained accessible after system migration. The endpoint failed to enforce object-level authorization, allowing an authenticated user to access another user's account-related information by manipulating an object identifier.

All testing was conducted within the authorized scope of the program.

---

## Methodology

I used a manual cross-account testing approach with two researcher-controlled accounts:

1. Established normal endpoint behavior using Account A.
2. Identified an object identifier used by the endpoint to retrieve account-related data.
3. Substituted the identifier with one belonging to Account B.
4. Sent the request using Account A’s authenticated session.
5. Observed that the application returned data associated with Account B.
6. Confirmed that the endpoint did not perform proper server-side ownership validation.

---

## Root Cause

The backend trusted the client-supplied object identifier without verifying that the requested resource belonged to the authenticated user. The issue was present on a deprecated endpoint, suggesting inconsistent authorization enforcement after migration.

This is a classic Broken Access Control vulnerability, specifically Insecure Direct Object Reference.

---

## Impact

An authenticated attacker could access unauthorized account-related information, creating privacy and potential fraud risks. Depending on the exposed data, the issue could also lead to compliance concerns and loss of user trust.

---

## Remediation

- Enforce server-side ownership validation for all object references.
- Apply centralized authorization middleware across active and legacy endpoints.
- Remove or properly secure deprecated endpoints.
- Add regression tests for cross-account access scenarios.
- Audit remaining legacy routes for similar authorization gaps.

---

## Lesson Learned

Deprecated endpoints can remain hidden attack surfaces if authorization controls are not consistently enforced. Authentication alone is not sufficient; object-level authorization must be explicitly validated.

---

## Responsible Disclosure Note

Sensitive technical details, including exact endpoints, parameter names, tokens, and user data, have been sanitized. Testing was performed exclusively using researcher-controlled accounts, and no unauthorized third-party data was intentionally accessed, retained, modified, or disclosed.
