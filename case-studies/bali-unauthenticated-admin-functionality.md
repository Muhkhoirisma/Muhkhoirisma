# Case Study: Unauthenticated Administrative Functionality

**Target:** Bali Provincial Government (Pemerintah Provinsi Bali)  
**Program Type:** Coordinated Disclosure — Government Agency  
**Category:** Broken Access Control, Missing Authentication Enforcement  
**Result:** Accepted — Official Certificate of Appreciation  
**Testing Mode:** Authorized / coordinated security testing within disclosure scope  

---

## Summary

During authorized security testing of a public-facing government application, I identified an administrative product-import function that could be reached and invoked **without any authentication**. The route was not protected by the same access-control enforcement applied to the rest of the application, leaving a privileged administrative capability exposed to unauthenticated callers.

The finding was responsibly disclosed through the official channel and acknowledged with an **Official Certificate of Appreciation**. No production data was modified, and no third-party records were accessed during validation.

Exact endpoints, parameters, and internal references have been sanitized.

---

## Context

The application exposes public UMKM product listings managed through an administrative back-end. Administrative capabilities—such as importing or updating product records—are expected to be available only to authenticated staff.

While mapping the surface within the agreed scope, I observed that one administrative import function did not appear to be gated by the authentication/authorization layer used elsewhere.

> Note on classification: this is often labeled “authentication bypass”, but the mechanism here is the **absence of authN/authZ enforcement on a privileged route**, not a flaw in the login flow itself. It is therefore framed as Broken Access Control.

---

## Methodology

Testing followed a **non-destructive, observation-first** approach appropriate for a government target:

1. **Surface mapping** — Enumerated publicly reachable routes within scope, including administrative-looking paths.
2. **Authentication baseline** — Confirmed normal flows require a session, establishing the expected control.
3. **Unauthenticated invocation** — Sent requests to the import function with **no** session/credential, observing whether the server enforced authentication.
4. **Non-destructive validation** — Verified the missing auth gate by response behavior only, **without** uploading records or altering live data.
5. **Impact reasoning** — Assessed what an attacker *could* do if chaining this with valid input, without performing the modification.
6. **Coordinated disclosure** — Reported via the official channel with sanitized evidence and remediation guidance.

> No production data was created, modified, deleted, or exfiltrated. Validation was limited to confirming the endpoint did not require authentication.

---

## Observation

The import function responded to unauthenticated requests in a way indicating the auth guard was **not applied** to this route.

Simplified:

```text
Flawed:
Request reaches admin route -> execute import logic without authN/authZ check

Expected:
Request reaches admin route -> verify session + admin permission -> allow or reject
```

This is a failure to **enforce** access control on a privileged route.

---

## Root Cause

Missing authentication/authorization enforcement on an administrative route.

Likely factors:

- **Route not covered by the global auth guard** — the import endpoint sits outside the middleware/policy protecting other admin functions.
- **Security by obscurity** — treated as “internal/hidden” and left unprotected, assuming nobody would find it.
- **Deployment/migration gap** — admin capability inadvertently exposed when public and internal surfaces share a host/routing layer.

In OWASP terms this maps primarily to **Broken Access Control (A01)**.

---

## Impact

Because the exposed capability is administrative, impact centers on **integrity and availability** of public data rather than confidentiality of PII:

- Unauthorized creation/modification/disruption of public UMKM product records.
- Potential publication of false or manipulated listing information to citizens.
- Reputational risk and erosion of public trust in the portal.
- Possible compliance/audit concerns for a government information system.

Severity is elevated because **no authentication is required at all**, widening the attacker pool to any internet-reachable party.

---

## Remediation Recommendations

- **Enforce authN + authZ globally** — all admin routes must pass the same guard; no privileged route reachable unauthenticated.
- **Deny by default** — new admin endpoints protected unless explicitly and reviewably opened.
- **Do not rely on hidden routes** — “internal-only” paths need active protection, not secrecy.
- **Layer restriction where feasible** — bind admin functions to internal network/VPN/mTLS in addition to app-level auth.
- **Audit the full admin surface** — review every administrative/import/bulk endpoint for the same gap.
- **Add regression tests** — assert unauthenticated calls to admin routes are rejected.

---

## Detection Opportunities

Monitor for:

- requests to admin paths with no session/identity;
- import/bulk invocations from unauthenticated sources;
- unexpected successful responses on routes that should always require auth;
- WAF/gateway alerts on admin-endpoint access from the public internet.

---

## Lessons Learned

1. **Hidden ≠ protected.** Unguarded admin routes are a classic Broken Access Control trap.
2. **Enforcement must be global, not per-route.** One unprotected privileged route negates the rest of the auth model.
3. **Government targets demand extra care.** Non-destructive validation and coordinated disclosure protect both the system and the researcher.
4. **Appreciation is a strong signal.** An official certificate reflects ethical coordination with a public institution—weight beyond a monetary bounty.
5. **Integrity findings matter.** Not every high-value issue leaks PII; compromising trustworthiness of public data is serious on its own.

---

## Outcome

- **Status:** Accepted  
- **Recognition:** Official Certificate of Appreciation from the agency  
- **Disclosure:** Coordinated through the official government channel  
- **Data Integrity:** No production data modified; validation non-destructive  
- **Public Detail Level:** Sanitized to protect endpoints, parameters, and internal references  

---

## Responsible Disclosure Note

All testing was conducted within the agreed disclosure scope and coordinated with the agency through official channels.

Validation was strictly **non-destructive**: no product records were created, modified, deleted, or exfiltrated, and no third-party data was accessed.

Sensitive technical details—including exact endpoints, parameters, and internal references—have been redacted to comply with responsible disclosure practices and to protect the integrity of a public government system.
