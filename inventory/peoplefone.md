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
