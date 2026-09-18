# Case Study: UUID-Based Broken Access Control

**Target:** NBA Identity  
**Platform:** HackerOne  
**Category:** Broken Access Control, IDOR, Missing Authorization  
**Result:** Valid Vulnerability, Duplicate  
**Testing Mode:** Authorized manual security testing  

---

## Summary

During authorized manual testing of an identity/profile API, I identified an authorization weakness where profile metadata belonging to another user could be accessed by manipulating the user identifier supplied to the API.

The endpoint returned profile metadata without verifying that the requested identifier belonged to the authenticated user. Testing was performed exclusively using researcher-controlled accounts.

The issue was confirmed as a valid vulnerability and marked as duplicate because the same authorization weakness had already been reported in an earlier submission. Although no bounty was awarded, the report independently reproduced the same broken access control behavior.

---

## Context

The tested platform used user identifiers, including UUID-style identifiers, to reference profile-related resources.

A common misconception in application security is:

> UUIDs are hard to guess, so they can be treated as access control.

That assumption is unsafe. A UUID may reduce predictability, but it does not replace server-side authorization checks.

During testing, I observed that the endpoint relied on the supplied identifier to fetch profile metadata, but did not consistently validate ownership against the authenticated session.

---

## Methodology

I used a manual cross-account validation approach:

1. Created and used two researcher-controlled accounts.
2. Authenticated as Account A.
3. Called the profile metadata endpoint using Account A’s own identifier.
4. Observed the normal response structure.
5. Replaced Account A’s identifier with Account B’s identifier.
6. Sent the request using Account A’s authenticated session.
7. Observed that the endpoint returned profile metadata associated with Account B.
8. Confirmed that the application did not enforce proper object-level authorization.

---

## Observation

The endpoint authenticated the requester successfully, but failed to verify whether the requested profile resource belonged to that requester.

Simplified:

```text
Flawed:
Authenticated user requests profile by identifier -> return profile metadata

Expected:
Authenticated user requests profile by identifier -> verify identifier belongs to user/session -> return or deny
```

This is a classic object-level authorization failure.

---

## Root Cause

The root cause was insufficient object-level authorization on a profile metadata endpoint.

Specifically:

1. The endpoint accepted a user-supplied identifier.
2. The identifier was used to retrieve profile metadata.
3. The backend did not verify that the requested identifier matched the authenticated user or an allowed relationship.
4. As a result, one authenticated user could access another user’s profile metadata.

Using UUIDs as identifiers does not inherently secure the resource. Authorization must still be enforced on the server side.

---

## Impact

An authenticated attacker could retrieve another user’s profile metadata due to insufficient authorization checks.

Potential impacts include:

- unauthorized disclosure of profile information;
- privacy violation;
- user enumeration or correlation attacks;
- increased risk of social engineering;
- erosion of trust in the identity platform.

The severity depends on the sensitivity of the exposed metadata, but the underlying issue is a clear Broken Access Control vulnerability.

---

## Remediation Recommendations

- Enforce server-side ownership validation for every profile resource request.
- Do not treat UUIDs as secrets or access-control mechanisms.
- Apply centralized authorization middleware for object-level access checks.
- Return consistent authorization errors without leaking whether a resource exists.
- Add regression tests for cross-account profile access scenarios.
- Audit related endpoints that accept user identifiers, organization identifiers, or session-linked resources.

---

## Detection Opportunities

Defensive teams can monitor for:

- authenticated users requesting profile resources not associated with their account;
- repeated identifier substitution attempts;
- unusual spikes in successful profile metadata requests;
- access patterns where requester identity and resource owner do not match.

---

## Lessons Learned

1. **UUIDs are identifiers, not authorization.**  
   Unpredictability is not access control.

2. **Authentication is not authorization.**  
   A valid session does not grant access to every object.

3. **Object-level authorization must be explicit.**  
   Every resource reference needs ownership or permission validation.

4. **Duplicate findings still validate real issues.**  
   The vulnerability was already known, but the submission independently reproduced the same flaw.

5. **Profile metadata can be sensitive even without obvious PII.**  
   Correlation, enumeration, and identity context can create real risk.

---

## Outcome

- **Status:** Valid Vulnerability  
- **Disposition:** Duplicate  
- **Bounty:** Not awarded due to duplicate status  
- **Disclosure:** Reported responsibly through HackerOne  
- **Public Detail Level:** Sanitized to protect sensitive implementation and user data  

---

## Responsible Disclosure Note

All testing was conducted within the authorized scope of the HackerOne program. The research used only researcher-controlled accounts. No unauthorized third-party data was intentionally accessed, retained, modified, or disclosed. Sensitive technical details have been redacted to comply with responsible disclosure practices.
