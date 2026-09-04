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
