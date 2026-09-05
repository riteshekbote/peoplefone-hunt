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
