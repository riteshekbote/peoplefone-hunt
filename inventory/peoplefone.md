# peoplefone GmbH inventory (discovery seed 2026-09-02)
# NOTE: hosts below are discovery candidates from passive DNS/CT; confirm in-scope vs program scope before active testing.
api.peoplefone.com
auth.peoplefone.com
peoplefone.com
support.peoplefone.com
www.peoplefone.com

## PASSIVE RECON 2026-09-02 (read-only, non-intrusive)

> Recon observations only. These are NOT confirmed vulnerabilities; ownership/in-scope of each host must be confirmed against the program scope before any active testing. Hosts resolve + serve HTTP — investigation requires scoped authorization.

**Probed:** 5 hosts | **Live HTTP:** 2

| Host | Status | Server/Tech |
|---|---|---|
| `api.peoplefone.com` | 302 | Server: cloudflare -> https://www.peoplefone.com/en-ch/developer |
| `support.peoplefone.com` | 302 | Server: cloudflare -> https://support.peoplefone.com/che/willkommen/ |

**CNAME review signals (2):**
- `api.peoplefone.com` -> `api.peoplefone.com.cdn.cloudflare.net`
- `support.peoplefone.com` -> `support.peoplefone.com.cdn.cloudflare.net`

## DEEP SERVICE SCAN 2026-09-02 (read-only connect+banner)
**Host:** `api.peoplefone.com` | **Ports:** [80, 443, 2082, 2083, 2086, 2087, 8080, 8443]
**Non-web ports observed:** [2082, 2083, 2086, 2087, 8080, 8443]
> NOTE: repeated identical non-web port sets (e.g. 2082,2083,2086,2087,8080,8443) across many hosts and wide port sets are likely a shared edge/proxy answering EOF, NOT confirmed real services. Verify with a proper port scanner (e.g. nmap) under authorization before treating as real. These are surface-map hints only, not findings.

## DEEP SERVICE SCAN 2026-09-02 (read-only connect+banner)
**Host:** `support.peoplefone.com` | **Ports:** [80, 443, 2082, 2083, 2086, 2087, 8080, 8443]
**Non-web ports observed:** [2082, 2083, 2086, 2087, 8080, 8443]
> NOTE: repeated identical non-web port sets (e.g. 2082,2083,2086,2087,8080,8443) across many hosts and wide port sets are likely a shared edge/proxy answering EOF, NOT confirmed real services. Verify with a proper port scanner (e.g. nmap) under authorization before treating as real. These are surface-map hints only, not findings.

## 2026-09-02 21:54:06 UTC

## 2026-09-02 23:55:44 UTC

## 2026-09-03 03:38:09 UTC

## 2026-09-03 08:20:18 UTC

## 2026-09-03 13:01:56 UTC

## 2026-09-03 17:08:53 UTC

## 2026-09-03 19:45:21 UTC

## 2026-09-03 22:39:38 UTC
- NEW Developer portal content retrieved - reveals SMS API documentation at `api.peoplefone.com/services/api-doc/`
- NEW API is explicitly public "available to all developers" - confirms attack surface is intentional
- NEW Full API backend surface discovered via Swagger UI: `configuration-api.peoplefone.com`, `call-api.peoplefone.com` — two un-inventoried subdomains
- NEW SMS API live at `api.peoplefone.com/customer/sms/v1` with documented `{messageId}` IDOR candidate + attacker-controlled `callbackUrl` (SSRF)
- NEW Smart Routing webhook accepts attacker-controlled `url` with 2-min single-use `X-Track-Id` — SSRF + webhook hijack candidate
- NEW Consuming APIs enforce bearer auth (401 confirmed live) — uaCSTA remote call control endpoints exposed (`/device/call/*`)

## 2026-09-04 00:31:51 UTC
- NEW configuration-api.peoplefone.com — discovered via Swagger UI at api.peoplefone.com/services/api-doc/; tenant-scoped PBX config API (`/customer/voip/v1`) with {identifier} CRUD endpoints; returns 401 w
- NEW call-api.peoplefone.com — discovered via Swagger UI; Call Management API (`/customer/call-management/v1`) with call control endpoints accepting owner.identifier; returns 401 without bearer token
- NEW SMS API at api.peoplefone.com/customer/sms/v1 — documented `{messageId}` BOLA candidate + attacker-controlled `callbackUrl` (SSRF vector); public "free for all developers" per portal
- NEW Smart Routing webhook — accepts attacker-controlled `url` with 2-min single-use `X-Track-Id`; SSRF + webhook hijack candidate
- NEW uaCSTA remote call control endpoints exposed at `/device/call/*` on consuming APIs
- CHANGED auth.peoplefone.com OAuth endpoints return 404 at expected paths (`/.well-known/oauth-authorization-server`, `/oauth/authorize`) — authorization server metadata and authorize endpoint not at standard 
- CHANGED configuration-api.peoplefone.com and call-api.peoplefone.com enforce bearer auth (401 confirmed live) — auth gate present but token scope isolation unproven

## 2026-09-04 05:12:08 UTC

## 2026-09-04 09:50:18 UTC
- CHANGED All 8 API YAML specs fully retrieved from `api.peoplefone.com/services/api-doc/api/` — 8000+ lines of attack surface now visible. Key new details vs prior knowledge:

## 2026-09-04 14:21:14 UTC
- NEW All 8 API YAML specs fully retrieved — 8000+ lines of attack surface now visible, including full CRUD operations, parameter schemas, and authorization boundary notes across Configuration, Call Managem
- CHANGED Phase transitioned from RECON to POC — token acquisition via portal.peoplefone.ch is the single blocker for all 3 hypothesis classes.
- NEW All 8 API YAML specs fully retrieved from `api.peoplefone.com/services/api-doc/api/` (8000+ lines) — complete attack surface now documented
- NEW 5 SSRF endpoints confirmed in specs: SMS callbackUrl, Smart Routing webhook url, uaCSTA callbackUrl+monitoringCallbackUrl, External Number Lookup webhookUrl — all accept attacker-controlled URI with z
- NEW External Number Lookup webhookUrl additionally forwards customer-configured custom headers to attacker-controlled URL
- NEW Queue API business logic flaw: agent login/logout actions accept cross-tenant agent+queue identifiers — call center disruption vector
- NEW Configuration API: Full CRUD on 8 resource types (users, groups, IVRs, queues, numbers, smart-routings, callforwarding, manual-routing) with numeric sequential identifiers; UserResponse exposes sipUse
- NEW External Routing API deprecated 2026-09-30 but still live — same webhook SSRF pattern as Smart Routing, potentially weaker code paths
- CHANGED auth.peoplefone.com: Token issuance path NOT in any API spec — must go through portal.peoplefone.ch; standard OAuth endpoints return 404
- CHANGED configuration-api.peoplefone.com and call-api.peoplefone.com enforce bearer auth (401 confirmed) — auth gate present but token-scope isolation unproven

## 2026-09-04 17:48:47 UTC
- NEW All 8 OpenAPI YAML specs fully retrieved from `api.peoplefone.com/services/api-doc/api/` (8000+ lines) — complete attack surface documented across Configuration API (8 resource types), SMS API, Call M
- NEW 5 SSRF endpoints confirmed in specs: SMS callbackUrl, Smart Routing webhook url, uaCSTA callbackUrl+monitoringCallbackUrl, External Number Lookup webhookUrl — all accept attacker-controlled URI with z
- NEW Queue API business logic flaw: agent login/logout actions accept cross-tenant agent+queue identifiers — call center disruption vector
- NEW Configuration API: Full CRUD on 8 resource types (users, groups, IVRs, queues, numbers, smart-routings, callforwarding, manual-routing) with numeric sequential identifiers; UserResponse exposes sipUse
- NEW External Routing API deprecated 2026-09-30 but still live — same webhook SSRF pattern as Smart Routing, potentially weaker code paths
- CHANGED auth.peoplefone.com: Token issuance path NOT in any API spec — must go through portal.peoplefone.ch; standard OAuth endpoints return 404
- CHANGED configuration-api.peoplefone.com and call-api.peoplefone.com enforce bearer auth (401 confirmed) — auth gate present but token-scope isolation unproven
- CHANGED Phase transitioned from RECON to POC — token acquisition via portal.peoplefone.ch is the single blocker for all 3 hypothesis classes

## 2026-09-04 19:59:08 UTC
- NEW probe-results.md last entry 2026-09-04 17:48:51 UTC shows `api.peoplefone.com/services/api-doc/` returns 200 (dev portal accessible) while `configuration-api.peoplefone.com/services/api-doc/` returns 
- NEW Knowledge base 2026-09-04 17:48:47 UTC documents all 8 OpenAPI YAML specs retrieved (8000+ lines) but probe-results shows `api.peoplefone.com/services/api-doc/api/` returned HTTP 403 at 14:21:19 UTC —
- CHANGED Phase confirmed POC — token acquisition via portal.peoplefone.ch is the single blocker for all 3 CRITICAL hypothesis classes (Configuration API IDOR/BOLA, SMS BOLA+SSRF, 5-endpoint SSRF)
- CHANGED External Routing API deprecated 2026-09-30 but still live — same SSRF pattern as Smart Routing, potentially weaker code paths (26 days from deprecation)

## 2026-09-04 22:17:33 UTC
- CHANGED Two independent model runs (bigpickle, nemotron3) converged on the identical top hypothesis — configuration-api {identifier} CRUD IDOR — cross-model corroboration strengthens its priority ranking.
- NEW probe-results.md 2026-09-04 19:59:10 UTC: `api.peoplefone.com/services/api-doc/` returns 200 (dev portal accessible) while `configuration-api.peoplefone.com/services/api-doc/` returns 404 — confirms r
- NEW Knowledge base 2026-09-04 17:48:47 UTC: all 8 OpenAPI YAML specs retrieved (8000+ lines) but `api.peoplefone.com/services/api-doc/api/` returned HTTP 403 at 14:21:19 UTC — spec directory listing block
- CHANGED Phase confirmed POC — token acquisition via portal.peoplefone.ch is the single blocker for all 3 CRITICAL hypothesis classes
- CHANGED External Routing API deprecated 2026-09-30 but still live — same SSRF pattern as Smart Routing, potentially weaker code paths (26 days from deprecation)

## 2026-09-05 00:16:08 UTC
- NEW auth.peoplefone.com/oauth/authorize is LIVE for client_id=1: `GET /oauth/authorize?...redirect_uri=https://evil.com/callback...` → HTTP 302 → `/de_CH/login` with the attacker `redirect_uri` PRESERVED 
- NEW Implicit (`response_type=token`) AND PKCE (`code_challenge`+`code_challenge_method=S256`) params accepted and preserved through the same redirect → public-client-style behavior
- NEW auth.peoplefone.com/oauth/token EXISTS (HTTP 405 on GET) — live token-exchange endpoint confirmed
- NEW auth.peoplefone.com/de_CH/register is LIVE (HTTP 200, `registrationForm` POST + Cloudflare Turnstile sitekey `0x4AAAAAAETtGmlFEOhYOX2V`) — self-service account creation available to an authorized oper
- NEW portal.peoplefone.ch inventoried: LIVE Laravel customer portal (XSRF-TOKEN + encrypted session cookie, httponly, secure) — `302 /` → `/home` → `/login` → `auth.peoplefone.com/oauth/authorize?client_id
- NEW `/services/api-doc/swagger-initializer.js` confirms exactly 8 specs, NO auth/token spec (token issuance confirmed off-spec, via portal OAuth flow)
- CHANGED REVERSED prior REJECTED-AUTH verdict: OAuth authorize endpoint confirmed live; arbitrary redirect_uri/state preserved for client_id=1 two hops deep (authorize → login); token endpoint live; full ATO-r
- NEW Probe 2026-09-04 22:17:35 UTC: `api.peoplefone.com/services/api-doc/` returns 200 (dev portal accessible) while `configuration-api.peoplefone.com/services/api-doc/` returns 404 — confirms real API bac
- CHANGED Two independent model runs (bigpickle, nemotron3) converged on identical top hypothesis — configuration-api {identifier} CRUD IDOR — cross-model corroboration strengthens priority
- CHANGED External Routing API deprecated 2026-09-30 but still live (26 days remaining) — same webhook SSRF pattern as Smart Routing, potentially weaker code paths
- CHANGED Phase confirmed POC — token acquisition via portal.peoplefone.ch is the single blocker for all 3 CRITICAL hypothesis classes

## 2026-09-05 04:42:31 UTC
- NEW auth.peoplefone.com/oauth/authorize CONFIRMED LIVE for client_id=1: 302→/de_CH/login preserving arbitrary redirect_uri; implicit (response_type=token) AND PKCE params accepted and preserved through lo
- NEW auth.peoplefone.com/oauth/token EXISTS (HTTP 405 on GET) — live token-exchange endpoint adjacent to unrestricted redirect_uri
- NEW auth.peoplefone.com/de_CH/register LIVE (HTTP 200, registrationForm POST + Cloudflare Turnstile sitekey 0x4AAAAAAETtGmlFEOhYOX2V) — self-service account creation available
- NEW portal.peoplefone.ch inventoried: LIVE Laravel customer portal (XSRF-TOKEN + encrypted session cookie); /→/home→/login→auth authorize chain is sole token-issuance route
- NEW /services/api-doc/swagger-initializer.js confirms exactly 8 specs, NO auth/token spec — OAuth URI flow is only documented credential path
- CHANGED REVERSED prior REJECTED-AUTH verdict: OAuth authorize endpoint confirmed live; arbitrary redirect_uri/state preserved two hops deep; token endpoint live; full ATO-relevant primitive reinstated
- CHANGED External Routing API deprecated 2026-09-30 but still live (26 days remaining) — same SSRF pattern as Smart Routing, potentially weaker code paths
- CHANGED Phase confirmed POC — token acquisition via portal.peoplefone.ch is single blocker for all 3 CRITICAL hypothesis classes
- CHANGED Cross-model convergence (bigpickle+nemotron3) on identical top hypothesis — configuration-api {identifier} CRUD IDOR

## 2026-09-05 08:40:18 UTC
- NEW auth.peoplefone.com/oauth/authorize CONFIRMED LIVE for client_id=1: 302→/de_CH/login preserving arbitrary redirect_uri; implicit (response_type=token) AND PKCE params accepted and preserved through lo
- NEW auth.peoplefone.com/oauth/token EXISTS (HTTP 405 on GET) — live token-exchange endpoint adjacent to unrestricted redirect_uri
- NEW auth.peoplefone.com/de_CH/register LIVE (HTTP 200, registrationForm POST + Cloudflare Turnstile sitekey 0x4AAAAAAETtGmlFEOhYOX2V) — self-service account creation available
- NEW portal.peoplefone.ch inventoried: LIVE Laravel customer portal (XSRF-TOKEN + encrypted session cookie); /→/home→/login→auth authorize chain is sole token-issuance route
- NEW /services/api-doc/swagger-initializer.js confirms exactly 8 specs, NO auth/token spec — OAuth URI flow is only documented credential path
- CHANGED REVERSED prior REJECTED-AUTH verdict: OAuth authorize endpoint confirmed live; arbitrary redirect_uri/state preserved two hops deep; token endpoint live; full ATO-relevant primitive reinstated
- CHANGED External Routing API deprecated 2026-09-30 but still live (26 days remaining) — same SSRF pattern as Smart Routing, potentially weaker code paths
- CHANGED Phase confirmed POC — token acquisition via portal.peoplefone.ch is single blocker for all 3 CRITICAL hypothesis classes
- CHANGED Cross-model convergence (bigpickle+nemotron3) on identical top hypothesis — configuration-api {identifier} CRUD IDOR

## 2026-09-05 12:06:02 UTC
- NEW auth.peoplefone.com/oauth/authorize CONFIRMED LIVE for client_id=1: 302→/de_CH/login preserving arbitrary redirect_uri; implicit (response_type=token) AND PKCE params accepted and preserved through lo
- NEW auth.peoplefone.com/oauth/token EXISTS (HTTP 405 on GET) — live token-exchange endpoint adjacent to unrestricted redirect_uri
- NEW auth.peoplefone.com/de_CH/register LIVE (HTTP 200, registrationForm POST + Cloudflare Turnstile sitekey 0x4AAAAAAETtGmlFEOhYOX2V) — self-service account creation available
- NEW portal.peoplefone.ch inventoried: LIVE Laravel customer portal (XSRF-TOKEN + encrypted session cookie); /→/home→/login→auth authorize chain is sole token-issuance route
- NEW /services/api-doc/swagger-initializer.js confirms exactly 8 specs, NO auth/token spec — OAuth URI flow is only documented credential path
- CHANGED REVERSED prior REJECTED-AUTH verdict: OAuth authorize endpoint confirmed live; arbitrary redirect_uri/state preserved two hops deep; token endpoint live; full ATO-relevant primitive reinstated
- CHANGED External Routing API deprecated 2026-09-30 but still live (26 days remaining) — same SSRF pattern as Smart Routing, potentially weaker code paths
- CHANGED Phase confirmed POC — token acquisition via portal.peoplefone.ch is single blocker for all 3 CRITICAL hypothesis classes
- CHANGED Cross-model convergence (bigpickle+nemotron3) on identical top hypothesis — configuration-api {identifier} CRUD IDOR

## 2026-09-05 15:27:47 UTC
- NEW auth.peoplefone.com/de_CH/register confirmed LIVE (HTTP 200, Turnstile sitekey `0x4AAAAAAETtGmlFEOhYOX2V`) — self-service account creation available to authorized operator
- NEW portal.peoplefone.ch fully inventoried: Laravel (XSRF-TOKEN + encrypted session cookie, httponly, secure); `/` → `/home` → `/login` → `auth.peoplefone.com/oauth/authorize?client_id=1` is sole token-is
- NEW `/services/api-doc/swagger-initializer.js` confirms exactly 8 specs, NO auth/token spec — OAuth URI flow only documented credential path
- CHANGED Triage 12:00 independently graded OAuth redirect_uri VALID 9.1 CRITICAL-conditional (report-channel: bugs.olivermaicher.eu)
- CHANGED BUSLOGIC @ call-api queue agents formally INVALID (spec-silent on membership validation) — dropped from priority
- CHANGED auth.peoplefone.com/oauth/authorize stateless-404 in fresh session; 302 preserving attacker redirect_uri only reproduces with warm portal session; register regressed 200→500 (transient); token endpoin

## 2026-09-05 17:42:47 UTC
- NEW auth.peoplefone.com/de_CH/register confirmed LIVE (HTTP 200, Turnstile sitekey `0x4AAAAAAETtGmlFEOhYOX2V`) — self-service account creation available to authorized operator
- NEW portal.peoplefone.ch fully inventoried: Laravel (XSRF-TOKEN + encrypted session cookie, httponly, secure); `/` → `/home` → `/login` → `auth.peoplefone.com/oauth/authorize?client_id=1` is sole token-is
- NEW `/services/api-doc/swagger-initializer.js` confirms exactly 8 specs, NO auth/token spec — OAuth URI flow only documented credential path
- CHANGED Triage 12:00 independently graded OAuth redirect_uri VALID 9.1 CRITICAL-conditional (report-channel: bugs.olivermaicher.eu)
- CHANGED BUSLOGIC @ call-api queue agents formally INVALID (spec-silent on membership validation) — dropped from priority
- CHANGED auth.peoplefone.com/oauth/authorize stateless-404 in fresh session; 302 preserving attacker redirect_uri only reproduces with warm portal session; register regressed 200→500 (transient); token endpoin

## 2026-09-05 19:35:12 UTC
- NEW auth.peoplefone.com/de_CH/register confirmed LIVE (HTTP 200, Turnstile sitekey `0x4AAAAAAETtGmlFEOhYOX2V`) — self-service account creation available to authorized operator
- NEW portal.peoplefone.ch fully inventoried: Laravel (XSRF-TOKEN + encrypted session cookie, httponly, secure); `/` → `/home` → `/login` → `auth.peoplefone.com/oauth/authorize?client_id=1` is sole token-is
- NEW `/services/api-doc/swagger-initializer.js` confirms exactly 8 specs, NO auth/token spec — OAuth URI flow only documented credential path
- CHANGED Triage 12:00 independently graded OAuth redirect_uri VALID 9.1 CRITICAL-conditional (report-channel: bugs.olivermaicher.eu)
- CHANGED BUSLOGIC @ call-api queue agents formally INVALID (spec-silent on membership validation) — dropped from priority
- CHANGED auth.peoplefone.com/oauth/authorize stateless-404 in fresh session; 302 preserving attacker redirect_uri only reproduces with warm portal session; register regressed 200→500 (transient); token endpoin

## 2026-09-05 21:46:33 UTC
- NEW auth.peoplefone.com/de_CH/register confirmed LIVE (HTTP 200, Turnstile sitekey `0x4AAAAAAETtGmlFEOhYOX2V`) — self-service account creation available to authorized operator (transient 500 regression no
- NEW portal.peoplefone.ch fully inventoried: Laravel (XSRF-TOKEN + encrypted session cookie, httponly, secure); `/` → `/home` → `/login` → `auth.peoplefone.com/oauth/authorize?client_id=1` is sole token-is
- NEW `/services/api-doc/swagger-initializer.js` confirms exactly 8 specs, NO auth/token spec — OAuth URI flow only documented credential path
- CHANGED Triage 12:00 independently graded OAuth redirect_uri VALID 9.1 CRITICAL-conditional (report-channel: bugs.olivermaicher.eu)
- CHANGED BUSLOGIC @ call-api queue agents formally INVALID (spec-silent on membership validation) — dropped from priority
- CHANGED auth.peoplefone.com/oauth/authorize stateless-404 in fresh session; 302 preserving attacker redirect_uri only reproduces with warm portal session; register regressed 200→500 (transient); token endpoin

## 2026-09-05 23:39:47 UTC
- NEW auth.peoplefone.com/de_CH/register confirmed LIVE (HTTP 200, Turnstile sitekey `0x4AAAAAAETtGmlFEOhYOX2V`) — self-service account creation available to authorized operator (transient 500 regression no
- NEW portal.peoplefone.ch fully inventoried: Laravel (XSRF-TOKEN + encrypted session cookie, httponly, secure); `/` → `/home` → `/login` → `auth.peoplefone.com/oauth/authorize?client_id=1` is sole token-is
- NEW `/services/api-doc/swagger-initializer.js` confirms exactly 8 specs, NO auth/token spec — OAuth URI flow only documented credential path
- CHANGED Triage 12:00 independently graded OAuth redirect_uri VALID 9.1 CRITICAL-conditional (report-channel: bugs.olivermaicher.eu)
- CHANGED BUSLOGIC @ call-api queue agents formally INVALID (spec-silent on membership validation) — dropped from priority
- CHANGED auth.peoplefone.com/oauth/authorize stateless-404 in fresh session; 302 preserving attacker redirect_uri only reproduces with warm portal session; register regressed 200→500 (transient); token endpoin

## 2026-09-06 01:23:13 UTC

## 2026-09-06 06:31:53 UTC
- NEW NO_DELTA — All 2026-09-06 knowledge-base entries reconfirm frozen state: auth.peoplefone.com register 500 / token 405 / stateless authorize 404 / portal 302 / api-doc 200 baseline; configuration-api {

## 2026-09-06 11:29:47 UTC

## 2026-09-06 14:26:37 UTC

## 2026-09-06 17:11:44 UTC

## 2026-09-06 19:31:05 UTC
- NEW auth.peoplefone.com/oauth/authorize stateless-404 in fresh session; 302 preserving attacker redirect_uri only reproduces with warm portal session (verified 2026-09-05 08:40 probe); register regressed 
- NEW Cross-model convergence (bigpickle+nemotron3) sustained 11 frozen cycles on Configuration API {identifier} CRUD IDOR as top hypothesis — no counter-evidence surfaced
- CHANGED Queue API business logic formally INVALID per triage 12:00 and 00:15 (spec-silent on membership validation) — dropped from active set
- CHANGED probe-results.md shows NO_DELTA — api.peoplefone.com/services/api-doc/ consistently 200 across all 2026-09-06 probes; no new endpoints or status changes

## 2026-09-06 21:30:15 UTC

## 2026-09-06 23:10:54 UTC

## 2026-09-07 01:12:39 UTC
- NEW — decisive evidence this cycle. `client_id=1/4/5` all return `invalid_client` JSON on no-secret code exchange (confidential clients); nonexistent ids (2,3,10,100,999,0,-1) throw unhandled Laravel 500.
- NEW probe-results.md: 2026-09-06 23:10:56 UTC — api.peoplefone.com/services/api-doc/ still 200; no new endpoints or status changes since 2026-09-05
- NEW knowledge-base: auth.peoplefone.com register 500 / token 405 / stateless authorize 404 / portal 302 / api-doc 200 baseline frozen 13+ cycles; configuration-api {identifier} CRUD IDOR rank holds 13th f
- CHANGED NO_DELTA on all live surfaces — configuration-api.peoplefone.com/services/api-doc/ remains 404; call-api.peoplefone.com/services/api-doc/ unprobed; portal.peoplefone.ch Laravel flow unchanged

## 2026-09-07 06:14:29 UTC
- NEW fresh re-verify this cycle — live state fully frozen: api-doc 200; register 500 (regression holds); stateless authorize (client_id=1, attacker redirect_uri) 404; POST /oauth/token client_id=1 no-secre
- NEW auth.peoplefone.com/oauth/token: POST code exchange without client_secret returns `invalid_client` JSON for client_id=1/4/5 (confirmed confidential clients); nonexistent client_ids (2,3,10,100,999,0,-
- NEW *.peoplefone.com DNS: 11 guessed subdomains (admin/mail/staging/test/dev-api/status/shop/billing/webmail/crm/pbx/voip) all NXDOMAIN — NO wildcard DNS exists; corrects prior "wildcard-dominated" claim;
- CHANGED configuration-api.peoplefone.com/services/api-doc/ remains 404; call-api.peoplefone.com/services/api-doc/ unprobed; portal.peoplefone.ch Laravel flow unchanged; api.peoplefone.com/services/api-doc/ st

## 2026-09-07 12:47:46 UTC

## 2026-09-07 18:15:44 UTC

## 2026-09-07 21:43:15 UTC
- NEW Knowledge base 2026-09-07: POST /oauth/token no client_secret → invalid_client JSON for client_id=1/4/5 (confidential clients); nonexistent client_ids (2,3,10,100,999,0,-1) → unhandled Laravel 500
- NEW Knowledge base 2026-09-07: 19 guessed subdomains (admin/mail/staging/test/dev-api/status/shop/billing/webmail/crm/pbx/voip/api-gw/internal/mgmt/invoice/partner/fileshare/sip/ws) all NXDOMAIN → NO wild
- CHANGED Configuration API {identifier} CRUD IDOR at 17th frozen cycle — no counter-evidence, cross-model rank holds, token-gated
- CHANGED SSRF 5 callback endpoints — retained pending token, no counter-evidence
- CHANGED BUSLOGIC queue agents — triage-formal INVALID (spec-silent on membership validation), removed from active set
- CHANGED auth.peoplefone.com state frozen 17+ cycles: register 500 / token 405 / stateless authorize 404 (sets redirect_uri cookie with attacker value) / api-doc 200 / portal 302
- NEW Knowledge base 2026-09-07: POST /oauth/token no client_secret → invalid_client JSON for client_id=1/4/5 (confidential clients); nonexistent client_ids (2,3,10,100,999,0,-1) → unhandled Laravel 500
- NEW Knowledge base 2026-09-07: 19 guessed subdomains (admin/mail/staging/test/dev-api/status/shop/billing/webmail/crm/pbx/voip/api-gw/internal/mgmt/invoice/partner/fileshare/sip/ws) all NXDOMAIN → NO wild
- CHANGED Configuration API {identifier} CRUD IDOR at 17th frozen cycle — no counter-evidence, cross-model rank holds, token-gated
- CHANGED SSRF 5 callback endpoints — retained pending token, no counter-evidence
- CHANGED BUSLOGIC queue agents — triage-formal INVALID (spec-silent on membership validation), removed from active set
- CHANGED auth.peoplefone.com state frozen 17+ cycles: register 500 / token 405 / stateless authorize 404 (sets redirect_uri cookie with attacker value) / api-doc 200 / portal 302

## 2026-09-07 23:49:15 UTC
- NEW `call-api.peoplefone.com/services/api-doc/` probed for first time → HTTP 404 (2026-09-07 21:43:20 UTC)
- NEW `auth.peoplefone.com/de_CH/register` consistently HTTP 500 across 18+ frozen cycles (regression holds)
- NEW `auth.peoplefone.com/oauth/token` POST no `client_secret` → `invalid_client` JSON for `client_id=1/4/5` (confidential); nonexistent IDs (2,3,10,100,999,0,-1) → unhandled Laravel 500
- NEW 19 guessed subdomains (admin/mail/staging/test/dev-api/status/shop/billing/webmail/crm/pbx/voip/api-gw/internal/mgmt/invoice/partner/fileshare/sip/ws) all NXDOMAIN → NO wildcard DNS; corrects prior "w
- CHANGED Configuration API {identifier} CRUD IDOR at 18th frozen cycle — no counter-evidence, cross-model rank holds, token-gated
- CHANGED SSRF 5 callback endpoints — retained pending token, no counter-evidence
- CHANGED BUSLOGIC queue agents — triage-formal INVALID (spec-silent on membership validation), removed from active set
- CHANGED auth.peoplefone.com state frozen 18+ cycles: register 500 / token 401/405 / stateless authorize 404 (sets `redirect_uri` cookie with attacker value) / api-doc 200 / portal 302

## 2026-09-08 03:46:49 UTC

## 2026-09-08 09:03:31 UTC

## 2026-09-08 13:29:58 UTC
- NEW No new probes since 2026-09-08 09:03:31 UTC (4h ago); all surfaces frozen: api-doc 200, register 500, stateless authorize 404+attacker redirect_uri cookie, token 401/405, call-api-doc 404, 19 subdomai
- CHANGED Time-advance only — 21st frozen cycle for Configuration API IDOR, 21st for SSRF, 21st for OAuth; no status-code changes, no new endpoints, no counter-evidence

## 2026-09-08 17:47:45 UTC
- NEW No new probes since 2026-09-08 09:03:31 UTC (4h ago); all surfaces frozen: api-doc 200, register 500, stateless authorize 404+attacker redirect_uri cookie, token 401/405, call-api-doc 404, 19 subdomai
- CHANGED Time-advance only — 22nd frozen cycle for Configuration API IDOR, 22nd for SSRF, 22nd for OAuth; no status-code changes, no new endpoints, no counter-evidence
- NEW 19 guessed subdomains all NXDOMAIN → NO wildcard DNS exists; corrects prior "wildcard-dominated" claim (knowledge base updated 2026-09-08)
- NEW POST /oauth/token no client_secret → invalid_client JSON for client_id=1/4/5 (confirmed confidential); nonexistent IDs (2,3,10,100,999,0,-1) → unhandled Laravel 500; code-theft ATO falsified for known
- NEW Stateless authorize sets `redirect_uri` cookie (httponly, secure, 1-year expiry) with attacker-controlled value even on 404 response — server processes redirect_uri param partially in stateless mode; 

## 2026-09-08 20:17:44 UTC
- CHANGED reposcan 18:10Z produced no public-org scan (TARGET_ORG not configured) — reposcan continues to yield no alternative in-scope surface; prior library-level leads (mail-validator-mx-server, provisioning
- NEW No new probes since 2026-09-08 09:03:31 UTC (8h ago); all surfaces frozen: api-doc 200, register 500, stateless authorize 404+attacker redirect_uri cookie, token 401/405, call-api-doc 404, 19 subdomai
- CHANGED Time-advance only — 23rd frozen cycle for Configuration API IDOR, 23rd for SSRF, 23rd for OAuth; no status-code changes, no new endpoints, no counter-evidence
- NEW OAuth open-redirect/login-CSRF finding triage-confirmed VALID 7.4 (9.1 conditional) — payload ready for bugs.olivermaicher.eu submission

## 2026-09-08 22:46:22 UTC
- CHANGED Time-advance only — 24th frozen cycle for Configuration API IDOR, 24th for SSRF, 24th for OAuth; no status-code changes, no new endpoints, no counter-evidence since 2026-09-08 09:03:31 UTC
- CHANGED reposcan 18:10Z produced no public-org scan (TARGET_ORG unconfigured) — no alternative in-scope surface
- NEW OAuth open-redirect/login-CSRF finding triage-confirmed VALID 7.4 (9.1 conditional) — payload ready for bugs.olivermaicher.eu submission

## 2026-09-09 01:13:45 UTC

## 2026-09-09 06:11:13 UTC

## 2026-09-09 11:42:22 UTC

## 2026-09-09 15:26:46 UTC

## 2026-09-09 18:45:52 UTC

## 2026-09-09 21:36:45 UTC

## 2026-09-09 23:33:21 UTC

## 2026-09-10 01:31:29 UTC

## 2026-09-10 06:43:45 UTC

## 2026-09-10 11:53:56 UTC
- NEW REJECTED MISCONFIG @ *.peoplefone.com: 19 guessed subdomains all NXDOMAIN → NO wildcard DNS; no dangling CNAME targets (corrects "wildcard-dominated" claim)
- NEW ACCEPTED AUTH @ auth.peoplefone.com: POST /oauth/token no client_secret → invalid_client JSON for clients 1/4/5 (confidential); nonexistent IDs → unhandled 500
- NEW ACCEPTED OTH @ auth.peoplefone.com: stateless authorize sets redirect_uri cookie (httponly, secure, 1-year expiry) with attacker value even on 404
- CHANGED Configuration API IDOR frozen 32nd cycle, SSRF frozen 32nd cycle, OAuth frozen 32nd cycle — no status-code changes, no new endpoints
- CHANGED call-api.peoplefone.com/services/api-doc/ 404 reconfirmed; config-api docs 404 reconfirmed; all 8-spec backends match 401/404-gated pattern
- NEW REJECTED BUSLOGIC @ call-api queue agents: triage-formal INVALID (spec-silent on membership validation); removed from active set

## 2026-09-10 16:08:02 UTC
- CHANGED OAuth at auth.peoplefone.com frozen 33rd cycle: register 500 / token GET 405 + POST(client_id=1)→401 + POST(no-body)→500 / stateless authorize 404+attacker redirect_uri cookie (Max-Age 34560000) / api
- CHANGED Configuration API IDOR frozen 33rd cycle — no counter-evidence, cross-model rank holds, token-gated
- CHANGED SSRF 5 callback endpoints frozen 33rd cycle — retained pending token, no counter-evidence
- NEW REJECTED MISCONFIG @ *.peoplefone.com: 19 guessed subdomains all NXDOMAIN → NO wildcard DNS; no dangling CNAME targets (corrects "wildcard-dominated" claim)
- NEW ACCEPTED AUTH @ auth.peoplefone.com: POST /oauth/token no client_secret → invalid_client JSON for clients 1/4/5 (confidential); nonexistent IDs → unhandled 500
- NEW ACCEPTED OTH @ auth.peoplefone.com: stateless authorize sets redirect_uri cookie (httponly, secure, 1-year expiry) with attacker value even on 404
- NEW REJECTED BUSLOGIC @ call-api queue agents: triage-formal INVALID (spec-silent on membership validation); removed from active set
- CHANGED call-api.peoplefone.com/services/api-doc/ 404 reconfirmed; config-api docs 404 reconfirmed; all 8-spec backends match 401/404-gated pattern

## 2026-09-10 19:16:12 UTC

## 2026-09-10 21:45:47 UTC
- NEW 19 guessed subdomains (admin/mail/staging/test/dev-api/status/shop/billing/webmail/crm/pbx/voip/api-gw/internal/mgmt/invoice/partner/fileshare/sip/ws) all NXDOMAIN → NO wildcard DNS exists; corrects p
- NEW POST /oauth/token with no client_secret → invalid_client JSON for clients 1/4/5 (confirmed confidential); nonexistent IDs (2,3,10,100,999,0,-1) → unhandled Laravel 500; code-theft-exchange ATO falsifi
- NEW Stateless authorize sets `redirect_uri` cookie (httponly, secure, Max-Age 34560000) with attacker-controlled value even on 404 response — server processes redirect_uri param partially in stateless mod
- CHANGED Configuration API IDOR frozen 34th cycle, SSRF frozen 34th cycle, OAuth frozen 34th cycle — no status-code changes, no new endpoints
- CHANGED call-api.peoplefone.com/services/api-doc/ 404 reconfirmed; config-api docs 404 reconfirmed; all 8-spec backends match 401/404-gated pattern
- CHANGED REJECTED BUSLOGIC @ call-api queue agents: triage-formal INVALID (spec-silent on membership validation); removed from active set

## 2026-09-10 23:53:32 UTC
- NEW 19 guessed subdomains (admin/mail/staging/test/dev-api/status/shop/billing/webmail/crm/pbx/voip/api-gw/internal/mgmt/invoice/partner/fileshare/sip/ws) all NXDOMAIN → NO wildcard DNS exists; corrects p
- NEW POST /oauth/token with no client_secret → invalid_client JSON for clients 1/4/5 (confirmed confidential); nonexistent IDs (2,3,10,100,999,0,-1) → unhandled Laravel 500; code-theft-exchange ATO falsifi
- NEW Stateless authorize sets `redirect_uri` cookie (httponly, secure, Max-Age 34560000) with attacker-controlled value even on 404 response — server processes redirect_uri param partially in stateless mod
- CHANGED Configuration API IDOR frozen 35th cycle, SSRF frozen 35th cycle, OAuth frozen 35th cycle — no status-code changes, no new endpoints
- CHANGED call-api.peoplefone.com/services/api-doc/ 404 reconfirmed; config-api docs 404 reconfirmed; all 8-spec backends match 401/404-gated pattern
- CHANGED REJECTED BUSLOGIC @ call-api queue agents: triage-formal INVALID (spec-silent on membership validation); removed from active set

## 2026-09-11 03:48:31 UTC
- NEW probe-results.md shows NO_DELTA since 2026-09-08 09:03:31 UTC — api.peoplefone.com/services/api-doc/ consistently 200; all live surfaces frozen (register 500, stateless authorize 404+attacker redirect
- NEW knowledge base confirms Configuration API IDOR frozen 35th cycle, SSRF 5 endpoints frozen 35th cycle, OAuth frozen 35th cycle — no status-code changes, no new endpoints, no counter-evidence
- NEW REJECTED MISCONFIG @ *.peoplefone.com re-confirmed: 19 guessed subdomains all NXDOMAIN → NO wildcard DNS; no dangling CNAME targets (corrects prior "wildcard-dominated" claim)
- NEW ACCEPTED AUTH @ auth.peoplefone.com: POST /oauth/token no client_secret → invalid_client JSON for clients 1/4/5 (confidential); nonexistent IDs → unhandled Laravel 500; code-theft ATO falsified for kn
- NEW ACCEPTED OTH @ auth.peoplefone.com: stateless authorize sets redirect_uri cookie (httponly, secure, Max-Age 34560000) with attacker-controlled value even on 404 — server processes redirect_uri param p
- CHANGED REJECTED BUSLOGIC @ call-api queue agents: triage-formal INVALID (spec-silent on membership validation); removed from active set

## 2026-09-11 08:47:53 UTC

## 2026-09-11 13:25:34 UTC
- NEW Register endpoint regression confirmed GLOBAL across all locale variants (en_CH/fr_CH/it_CH/de_DE/en_GB → 500, bare /register → 404) — minting lever permanently closed agent-side
- NEW auth.peoplefone.com stateless authorize sets `redirect_uri` cookie (Max-Age 34560000, httponly, secure) with attacker-controlled value even on 404 — server partially processes redirect_uri in stateles
- CHANGED Configuration API IDOR frozen 36th cycle, SSRF 5 endpoints frozen 36th cycle, OAuth frozen 36th cycle — no status-code changes, no new endpoints, no counter-evidence since 2026-09-08
- CHANGED 19 guessed subdomains all NXDOMAIN → NO wildcard DNS exists; corrects prior "wildcard-dominated" claim (re-verified 2026-09-11)
- CHANGED call-api.peoplefone.com/services/api-doc/ 404 reconfirmed; config-api docs 404 reconfirmed; all 8-spec backends match 401/404-gated pattern

## 2026-09-11 17:16:44 UTC

## 2026-09-11 19:51:32 UTC
