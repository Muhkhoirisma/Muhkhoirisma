# Case Study: Missing Authorization on Booking Status Endpoint

**Target:** Agoda  
**Platform:** HackerOne  
**Category:** Broken Access Control, Missing Authorization  
**Result:** Valid Vulnerability, Duplicate  
**Testing Mode:** Authorized manual security testing  

---

## Summary

During authorized manual testing, I identified an authorization weakness on a booking status endpoint. The endpoint used a supplied polling token to retrieve booking-related information, but it did not properly verify whether the token belonged to the authenticated user.

By using two researcher-controlled accounts, I observed that replacing Account A’s token with Account B’s token caused the application to return booking metadata associated with Account B.

The issue was confirmed as a valid vulnerability. It was marked as duplicate because the same authorization weakness had already been reported in an earlier submission. Although no bounty was awarded, the submission independently reproduced the same broken access control behavior.

---

## Context

The tested feature appeared to support asynchronous booking status checking. In this type of flow, the client usually sends a token to repeatedly check the status of a booking operation.

The security assumption for such an endpoint should be:

> The token must be validated not only as a valid token, but also as a token owned by the authenticated user or session making the request.

During testing, the endpoint appeared to authenticate the user successfully, but failed to enforce proper object-level authorization between the authenticated session and the requested booking resource.

---

## Methodology

I used a manual cross-account authorization validation approach:

1. Created and used two researcher-controlled accounts.
2. Performed the normal booking status flow using Account A.
3. Captured the expected behavior of the endpoint and its polling token.
4. Sent a request using Account A’s authenticated session.
5. Replaced Account A’s polling token with Account B’s polling token.
6. Compared the responses.
7. Confirmed that the endpoint returned Account B’s booking metadata.

---

## Observation

The key observation was that the endpoint did not reject the request when the authenticated session and the supplied token belonged to different users.

In simplified form, the flawed behavior was:

```text
If request contains a valid polling token:
    return booking data associated with that token
```

The safer expected behavior should be:

```text
If request contains a valid polling token:
    verify that the token belongs to the authenticated user/session
    if yes:
        return booking data
    else:
        deny access
```

This indicated a missing object-level authorization check.

---

## Root Cause

The root cause was insufficient authorization validation on the booking status endpoint.

Specifically:

1. The endpoint accepted a client-supplied polling token.
2. The token was treated as the primary lookup key for booking data.
3. The application did not consistently verify that the token belonged to the authenticated user.
4. As a result, one authenticated user could retrieve another user’s booking metadata by substituting the token.

This is a Broken Access Control issue caused by missing object-level authorization.

---

## Impact

The vulnerability could allow an authenticated attacker to access another user’s booking-related metadata.

Potential impacts include:

- unauthorized disclosure of booking information;
- privacy violation;
- exposure of booking identifiers and status data;
- potential misuse of payment-related or self-service references;
- increased risk of social engineering or targeted fraud;
- erosion of user trust.

The exact severity depends on the sensitivity of the exposed data and whether tokens are predictable, enumerable, or reusable. However, the core issue remains a failure to enforce proper ownership validation.

---

## Remediation Recommendations

- Verify that every supplied polling token belongs to the authenticated user/session.
- Bind polling tokens to user context, session context, or booking owner.
- Return an appropriate authorization error when a valid token is used by an unauthorized user.
- Avoid exposing unnecessary payment or self-service references.
- Add cross-account regression tests for booking status endpoints.

---

## Lessons Learned

- Authentication is not authorization.
- A valid token does not automatically mean the requesting user owns the resource.
- Polling/status endpoints can hide access control flaws.
- Duplicate findings are still valid reproductions of real security issues.
- Cross-account testing is essential for discovering horizontal privilege escalation.

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
