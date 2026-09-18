# Case Study: IDOR / Broken Access Control on Deprecated API Endpoint

**Target:** Kredivo  
**Category:** IDOR, Broken Access Control  
**Result:** Accepted & Rewarded  

## Summary

During authorized manual API testing, I identified an authorization flaw on a deprecated endpoint that remained accessible after system migration. The endpoint failed to enforce object-level authorization, allowing an authenticated user to access another user's account-related information by manipulating an object identifier.

## Methodology

I used a manual cross-account testing approach with two researcher-controlled accounts. After establishing normal behavior with my own account, I replaced the object identifier with an identifier belonging to the second account. The application returned data associated with the other account, indicating missing ownership validation.

## Root Cause

The backend trusted the client-supplied object identifier without verifying that the requested resource belonged to the authenticated user. The issue was present on a deprecated endpoint, suggesting inconsistent authorization enforcement after migration.

## Impact

An authenticated attacker could access unauthorized account-related information, creating privacy and potential fraud risks.

## Remediation

- Enforce server-side ownership validation for all object references.
- Apply centralized authorization middleware.
- Remove or properly secure deprecated endpoints.
- Add regression tests for cross-account access scenarios.

## Lesson Learned

Deprecated endpoints can remain hidden attack surfaces if authorization controls are not consistently enforced. Authentication alone is not sufficient; object-level authorization must be explicitly validated.
