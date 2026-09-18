# Case Study: Exposed Go pprof Debug Endpoint

**Target:** Supra Security  
**Platform:** Vulnerability Disclosure Program  
**Category:** Information Disclosure, Security Misconfiguration, Exposed Debug Endpoint  
**Result:** Reported, Remediation Observed, Pending Formal Confirmation  
**Testing Mode:** Authorized manual security testing within disclosure scope  

---

## Summary

During authorized manual testing, I identified a publicly accessible Go profiling/debug interface on a production monitoring host. The endpoint exposed runtime profiling information that is generally intended for internal debugging and performance analysis, not for public access.

After responsible disclosure, the previously accessible debug interface was rechecked and was no longer publicly accessible. This indicates that the exposed endpoint had likely been restricted or removed. Formal vendor confirmation was still pending at the time of writing.

To comply with responsible disclosure, exact hostnames, internal paths, function names, and raw profiling outputs have been sanitized.

---

## Context

Go applications can expose profiling endpoints, commonly associated with `pprof`, to help developers analyze runtime behavior, goroutines, heap usage, CPU profiling, and execution paths.

These endpoints can be useful internally, but they become a security concern when exposed on production systems without authentication or network restriction.

The tested system appeared to expose a debugging/profiling interface publicly.

---

## Methodology

Testing followed a safe, observation-only approach:

1. **Endpoint enumeration** — Identified publicly reachable paths within the authorized scope.
2. **Debug interface discovery** — Observed that a Go profiling/debug endpoint was accessible without authentication.
3. **Safe observation** — Reviewed high-level profiling output only, without attempting exploitation or data exfiltration.
4. **Information classification** — Assessed what type of internal details were exposed.
5. **Responsible disclosure** — Reported the finding through the official channel.
6. **Remediation recheck** — Verified later that the endpoint was no longer publicly accessible.

No credentials, authentication tokens, or third-party user data were intentionally accessed or exfiltrated during testing.

---

## Observation

The exposed profiling interface revealed runtime and implementation details that could assist an attacker in reconnaissance.

Examples of the type of information exposed, described generically:

- internal application structure;
- Go function names;
- internal filesystem paths;
- execution flow hints;
- framework or library indicators;
- monitoring/query-related components.

This does not immediately equal remote code execution or data breach. However, it provides useful internal context that can support further targeted attacks.

---

## Root Cause

The root cause was insecure exposure of a production debugging/profiling endpoint.

Likely contributing factors:

1. **Debug interface enabled in production**  
   Profiling endpoints were left active on a publicly reachable service.

2. **Missing authentication or authorization**  
   The endpoint did not require a valid identity or administrative permission.

3. **Missing network restriction**  
   The endpoint was reachable from the public internet instead of being limited to internal networks, VPN, or localhost.

4. **Security misconfiguration**  
   A feature intended for internal diagnostics became externally accessible.

---

## Impact

The primary impact is **information disclosure**.

Potential effects include:

- attacker reconnaissance against the application stack;
- exposure of internal paths and function names;
- identification of libraries, frameworks, or services in use;
- support for follow-up attacks targeting known components;
- reduced attacker effort in understanding the application internals.

The severity in this case was assessed as informational to low, depending on the sensitivity of the exposed runtime data. No direct credential leakage or user data exposure was observed.

---

## Remediation Recommendations

- Disable profiling/debug endpoints in production unless strictly required.
- If needed, bind them to localhost or an internal management network only.
- Require strong authentication and authorization for any debugging interface.
- Use network-level controls such as firewall rules, VPN, zero-trust access, or reverse-proxy restrictions.
- Add deployment checks to prevent debug endpoints from being exposed publicly.
- Monitor for external requests to known profiling paths.
- Review other production services for similar diagnostic exposure.

---

## Detection Opportunities

Defensive teams can monitor for:

- public requests to profiling/debug paths;
- successful responses from endpoints that should be internal-only;
- repeated access to runtime diagnostic interfaces;
- WAF or gateway rules blocking known debug endpoints from untrusted networks.

---

## Lessons Learned

1. **Debug features are not harmless.**  
   Even if they do not directly expose credentials, they can reveal internal structure useful to attackers.

2. **Production should not expose internal diagnostics publicly.**  
   Profiling endpoints belong behind strict network and identity controls.

3. **Information disclosure supports attack chains.**  
   Seemingly low-severity findings can become valuable reconnaissance for more targeted attacks.

4. **Remediation observation matters.**  
   The endpoint was later no longer publicly accessible, showing responsible disclosure can lead to practical fixes even before formal confirmation.

5. **Sanitization is essential.**  
   Publishing raw internal paths, function names, or hostnames can create unnecessary risk.

---

## Outcome

- **Status:** Reported  
- **Remediation:** Endpoint no longer publicly accessible during recheck  
- **Formal Confirmation:** Pending at time of writing  
- **Bounty/Acknowledgment:** Not received at time of writing  
- **Public Detail Level:** Sanitized to protect hostnames, internal paths, function names, and raw outputs  

---

## Responsible Disclosure Note

All testing was conducted within the authorized scope of the vulnerability disclosure program. Testing was limited to safe observation of publicly accessible debugging information.

No credentials, authentication tokens, or third-party user data were intentionally accessed, retained, modified, or disclosed. Sensitive technical details—including exact hostnames, endpoints, internal paths, and profiling outputs—have been redacted to comply with responsible disclosure practices.
