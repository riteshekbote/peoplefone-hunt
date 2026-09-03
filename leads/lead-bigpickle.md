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
