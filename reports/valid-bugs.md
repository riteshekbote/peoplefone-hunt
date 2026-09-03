# Validated findings (running count 0)

- 5 lead(s) marked VALID at 2026-09-03 23:46:45 UTC
  - | Q4 Provable non-invasively? | NO — probe returned HTTP 404 on `/oauth/authorize?client_id=test&redirect_uri=...`. Cannot confirm endpoint exists or is vulnerable without valid `client_id` and a logi
  - **Verdict: HOLD** — Requires authenticated probe with valid `client_id` and portal login session to confirm. Current probe evidence is insufficient (404 = endpoint not found or misconfigured test para
  - | Q4 Provable non-invasively? | NO — probe returned HTTP 401. Requires valid bearer token + neighboring tenant identifiers to demonstrate cross-tenant access. |
  - | Q4 Provable non-invasively? | PARTIALLY — spec shows `{messageId}` in path, but probe didn't fetch live response body. Need valid token + enumerate neighbor IDs. |
  - | OAuth redirect_uri bypass | **HOLD** | Probe returned 404; needs valid client_id + login session to confirm |
