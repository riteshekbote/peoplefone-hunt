# Validated findings (running count 0)

- 5 lead(s) marked VALID at 2026-09-03 23:46:45 UTC
  - | Q4 Provable non-invasively? | NO — probe returned HTTP 404 on `/oauth/authorize?client_id=test&redirect_uri=...`. Cannot confirm endpoint exists or is vulnerable without valid `client_id` and a logi
  - **Verdict: HOLD** — Requires authenticated probe with valid `client_id` and portal login session to confirm. Current probe evidence is insufficient (404 = endpoint not found or misconfigured test para
  - | Q4 Provable non-invasively? | NO — probe returned HTTP 401. Requires valid bearer token + neighboring tenant identifiers to demonstrate cross-tenant access. |
  - | Q4 Provable non-invasively? | PARTIALLY — spec shows `{messageId}` in path, but probe didn't fetch live response body. Need valid token + enumerate neighbor IDs. |
  - | OAuth redirect_uri bypass | **HOLD** | Probe returned 404; needs valid client_id + login session to confirm |

- 7 lead(s) marked VALID at 2026-09-05 05:55:43 UTC
  - | Q2 Reachable | **PARTIAL** | 401 enforced on live endpoints; requires valid bearer token. Not unauth-accessible. "Low-priv" may apply if token-scope isolation is weak (spec says "user must be part o
  - | Q4 Non-invasive proof | **NO** | Spec analysis only. 235KB OpenAPI spec reveals 8 resource types with numeric sequential identifiers (20023, 20024, 2, 2000) and an explicit authorization boundary st
  - ### **VERDICT: VALID**
  - | Q2 Reachable | **PARTIAL** | All endpoints require valid bearer token (401 confirmed live). Not unauth-accessible. |
  - | Q2 Reachable | **PARTIAL** | Requires valid bearer token (401 enforced). SMS API is public ("free for all developers") which lowers token acquisition barrier, but still requires authentication. |
  - | 2 | OAuth redirect_uri bypass (client_id=1) | **VALID** | 9.1 CRITICAL (or 7.4 HIGH) | **Report to bugs.olivermaicher.eu** with HTTP 302 trace |
  - | 2 | OAuth redirect_uri bypass (client_id=1) | **VALID** | 9.1 CRITICAL |

- 4 lead(s) marked VALID at 2026-09-05 16:09:01 UTC
  - | Q2 Reachable? | PARTIAL | 401 enforced; requires valid bearer token. Not unauth-accessible. |
  - **Verdict: VALID**
  - | Q2 Reachable? | PARTIAL | All require valid bearer token (401 confirmed). Not unauth-accessible. |
  - | 2 | OAuth redirect_uri bypass (client_id=1) | **VALID** | **9.1 CRITICAL** | **Report to bugs.olivermaicher.eu now** |

- 4 lead(s) marked VALID at 2026-09-06 00:15:19 UTC
  - | Q2 Reachable | PARTIAL | 401 enforced; requires valid bearer token. Not unauth-accessible. |
  - **Verdict: VALID**
  - | Q2 Reachable | PARTIAL | All require valid bearer token (401 enforced) |
  - | 2 | OAuth redirect_uri bypass (client_id=1) | **VALID** | 9.1 CRITICAL | **Report to bugs.olivermaicher.eu** |

- 10 lead(s) marked VALID at 2026-09-08 00:30:00 UTC
  - [ ] Output verdicts with proof steps, impact, CVSS, channel for VALID leads
  - [ ] Output verdicts with proof steps, impact, CVSS, channel for VALID leads
  - [✓] Output verdicts with proof steps, impact, CVSS, channel for VALID leads
  - | Q7 | Would reasonable triager accept? | **Yes.** Open-redirect on login flow with `redirect_uri` cookie injection is a concrete, exploitable primitive. Prior triage in this repo graded VALID 9.1 CRI
  - **Verdict: VALID**
  - | Q3 | Real security impact? | **Minimal.** Out-of-scope explicitly lists "Descriptive error messages or headers (e.g. Stack Traces, banner grabbing)." This is information disclosure via error message
  - | Q2 | Attacker reachable? | **Partially.** 401 confirmed — bearer token required. Not unauthenticated. Requires valid operator token to test. |
  - | Q4 | Provable non-invasively? | **No.** Cannot verify IDOR without active write/read attempts using a valid bearer token against cross-tenant identifiers. Spec analysis alone is insufficient proof. 
  - | Q4 | Provable non-invasively? | **No.** Requires active POST with attacker-controlled callback URL and valid bearer token. Cannot verify without auth. |
  - | 1 | OAuth redirect_uri preservation / open-redirect + login-CSRF | **VALID** | 7.4 (9.1 conditional) | Yes — submit now |

- 6 lead(s) marked VALID at 2026-09-10 23:23:27 UTC
  - | Q3 Real impact? | CONDITIONAL — Cross-tenant CRUD on 8 resource types (users, groups, IVRs, queues, numbers, smart-routings, callforwarding, manual-routing); requires valid bearer token |
  - | Q4 Provable non-invasively? | NO — Requires valid bearer token to invoke endpoints |
  - | Q7 Reasonable triager accept? | CONDITIONAL — 7.4 base, 9.1 if token scope is broad; triage-confirmed VALID per inventory entry |
  - **Verdict: VALID** — Meets all gates with conditional severity.
  - | Q3 Real impact? | LOW — POST without client_secret returns `invalid_client` JSON for valid client_ids; nonexistent IDs return unhandled Laravel 500 |
  - | OAuth redirect_uri | **VALID** | 7.4 (9.1 conditional) |
