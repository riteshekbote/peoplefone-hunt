# Hypotheses (ranked)

## RANKED HYPOTHESES 2026-09-02 21:54:06 UTC

## RANKED HYPOTHESES 2026-09-02 23:55:44 UTC

## RANKED HYPOTHESES 2026-09-03 03:38:09 UTC

## RANKED HYPOTHESES 2026-09-03 08:20:18 UTC

## RANKED HYPOTHESES 2026-09-03 13:01:56 UTC

## RANKED HYPOTHESES 2026-09-03 17:08:53 UTC
- [72] api.peoplefone.com: Developer Portal Hidden API Endpoints (from art/lead_bigpickle.txt)
- [65] auth.peoplefone.com: OAuth redirect_uri validation bypass on auth service (from art/lead_nemotron3.txt)
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://auth.peoplefone.com/.well-known/oauth-authorization-server
- NEXT(hypotheses-bigpickle.txt): PROBE: GET https://www.peoplefone.com/en-ch/developer (read-only, follow redirects, capture response content for developer portal analysis)
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: wildcard-dominated DNS with all CNAMEs pointing to managed Cloudflare CDN (per inventory) makes dangling CNAME takeover i
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: Dedicated auth subdomains high-value for session/token flaws
- LEARN: ACCEPTED IDOR @ api.peoplefone.com: Developer portals common source of API exposure
- LEARN: REJECTED MISCONFIG @ support.peoplefone.com: Low confidence, support portals typically non-critical

## RANKED HYPOTHESES 2026-09-03 19:45:21 UTC
- [72] api.peoplefone.com: Developer Portal Hidden API Endpoints (from art/lead_bigpickle.txt)
- [65] auth.peoplefone.com: OAuth redirect_uri validation bypass on auth service (from art/lead_nemotron3.txt)
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://auth.peoplefone.com/.well-known/oauth-authorization-server
- NEXT(hypotheses-bigpickle.txt): PROBE: GET https://www.peoplefone.com/en-ch/developer (read-only, follow redirects, capture response content for developer portal analysis)
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: wildcard-dominated DNS with all CNAMEs pointing to managed Cloudflare CDN (per inventory) makes dangling CNAME takeover i
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: Dedicated auth subdomains high-value for session/token flaws
- LEARN: ACCEPTED IDOR @ api.peoplefone.com: Developer portals common source of API exposure
- LEARN: REJECTED MISCONFIG @ support.peoplefone.com: Low confidence, support portals typically non-critical
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: Dedicated auth subdomains high-value for session/token flaws
- LEARN: ACCEPTED IDOR @ api.peoplefone.com: Developer portals common source of API exposure
- LEARN: REJECTED MISCONFIG @ support.peoplefone.com: Low confidence, support portals typically non-critical

## RANKED HYPOTHESES 2026-09-03 22:39:38 UTC
- [85] auth.peoplefone.com: OAuth redirect_uri validation bypass on auth service (from art/lead_nemotron3.txt)
- [78] api.peoplefone.com/services/api-doc/: SMS API Documentation Exposure (from art/lead_bigpickle.txt)
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://auth.peoplefone.com/oauth/authorize?client_id=1&redirect_uri=https://attacker.com/callback&response_type=code&scope=openid&state=<fresh_state
- NEXT(hypotheses-bigpickle.txt): PROBE: GET https://api.peoplefone.com/services/api-doc/ (read-only, capture full response content for API schema analysis)
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: OAuth authorize endpoint lacks redirect_uri allowlist validation for client_id=1; arbitrary redirect_uri accepted and prese
- LEARN: ACCEPTED IDOR @ configuration-api.peoplefone.com: Multi-tenant API exposes virtualUsers/{identifier} endpoints with explicit authorization boundary notes in spe
- LEARN: ACCEPTED IDOR @ call-api.peoplefone.com: Call control endpoints accept owner.identifier in body with authorization boundary notes
- LEARN: REJECTED MISCONFIG @ www.peoplefone.com: GraphQL introspection hypothesis invalidated — developer portal uses OpenAPI/Swagger, not GraphQL
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: Wildcard DNS dominated by Cloudflare CDN CNAMEs; no dangling third-party targets observed
- LEARN: ACCEPTED IDOR @ api.peoplefone.com: Developer portal explicitly links to public API documentation confirming attack surface
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: Dedicated auth subdomains high-value for session/token flaws
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: wildcard-dominated DNS with all CNAMEs pointing to managed Cloudflare CDN makes dangling CNAME takeover improbable
- LEARN: ACCEPTED IDOR @ api.peoplefone.com: Exposed Swagger UI reveals full SMS/Bola messageId endpoint surface with per-{messageId} access — high-value BOLA candidate
- LEARN: ACCEPTED SSRF @ api/call-api: Spec-documented attacker-controlled callbackUrl and Smart Routing webhook url constitute server-side-fetch SSRF vectors (post-auth
- LEARN: ACCEPTED IDOR @ configuration-api.peoplefone.com: Newly found tenant-scoped PBX config API (`/customer/voip/v1`) with {identifier} CRUD — IDOR/BOLA candidate
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: Swagger UI is protected by 401 on all real API backends; unauthenticated docs exposure is by-design dev portal, not stand

## RANKED HYPOTHESES 2026-09-04 00:31:51 UTC
- [75] api.peoplefone.com/customer/sms/v1/sms/messages/{messageId}: BOLA on SMS messageId (cross-tenant SMS disclosure) (from art/lead_nemotron3.txt)
- [62] api.peoplefone.com/services/api-doc/: SMS API OpenAPI spec exposes self-service token-issuance flow and messageId format (from art/lead_bigpickle.txt)
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://api.peoplefone.com/services/api-doc/ (read-only, capture full OpenAPI/Swagger JSON spec for SMS, Configuration, and Call Management APIs to e
- LEARN: ACCEPTED IDOR @ api.peoplefone.com: Exposed Swagger UI reveals full SMS/BOLA messageId endpoint surface with per-{messageId} access — high-value BOLA candidate
- LEARN: ACCEPTED SSRF @ api/call-api: Spec-documented attacker-controlled callbackUrl and Smart Routing webhook url constitute server-side-fetch SSRF vectors (post-auth
- LEARN: ACCEPTED IDOR @ configuration-api.peoplefone.com: Newly found tenant-scoped PBX config API (`/customer/voip/v1`) with {identifier} CRUD — IDOR/BOLA candidate
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: Swagger UI is protected by 401 on all real API backends; unauthenticated docs exposure is by-design dev portal, not stand
- LEARN: REJECTED AUTH @ auth.peoplefone.com: Standard OAuth endpoints (/.well-known/oauth-authorization-server, /oauth/authorize) return 404 — authorize endpoint likely

## RANKED HYPOTHESES 2026-09-04 05:12:08 UTC
- [80] configuration-api.peoplefone.com/customer/voip/v1/{virtualUsers,numbers,users,smart-routings,destinations,callforwarding}/{identifier}: IDOR/BOLA on Configuration API virtualUsers and tenant resources (from art/lead_nemotron3.txt)
- [78] configuration-api.peoplefone.com/customer/voip/v1/{users,numbers,virtualUsers}/{identifier}: IDOR/BOLA on configuration-api tenant-scoped {identifier} resources (from art/lead_bigpickle.txt)
- NEXT(hypotheses-nemotron3.txt): PROBE: With valid bearer token (from test account) GET https://api.peoplefone.com/customer/sms/v1/sms/messages → capture messageId format; then test sequential/
- NEXT(hypotheses-bigpickle.txt): PROBE: GET https://api.peoplefone.com/services/api-doc/ (read-only, capture full response body for OpenAPI/Swagger spec — extract token issuance endpoint, messa
- LEARN: ACCEPTED IDOR @ api.peoplefone.com: Exposed Swagger UI reveals full SMS/BOLA messageId endpoint surface with per-{messageId} access — high-value BOLA candidate
- LEARN: ACCEPTED SSRF @ api/call-api: Spec-documented attacker-controlled callbackUrl and Smart Routing webhook url constitute server-side-fetch SSRF vectors (post-auth
- LEARN: ACCEPTED IDOR @ configuration-api.peoplefone.com: Newly found tenant-scoped PBX config API (`/customer/voip/v1`) with {identifier} CRUD — IDOR/BOLA candidate
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: Swagger UI is protected by 401 on all real API backends; unauthenticated docs exposure is by-design dev portal, not stand
- LEARN: REJECTED AUTH @ auth.peoplefone.com: Standard OAuth endpoints (/.well-known/oauth-authorization-server, /oauth/authorize) return 404 — authorize endpoint likely
- LEARN: ACCEPTED IDOR @ call-api.peoplefone.com: Call control endpoints accept owner.identifier in body with explicit authorization boundary notes in spec
- LEARN: REJECTED AUTH @ auth.peoplefone.com: Standard OAuth endpoints return 404; authorize endpoint not at standard path; BLOCKED for automation
- LEARN: ACCEPTED IDOR @ configuration-api.peoplefone.com: 235KB spec with explicit authorization boundary notes + {identifier} CRUD — confirmed CRITICAL BOLA candidate
- LEARN: ACCEPTED IDOR @ api.peoplefone.com: SMS messageId endpoint surface confirmed in spec — cross-tenant disclosure viable if tenant isolation absent
- LEARN: ACCEPTED SSRF @ api/call-api: callbackUrl + Smart Routing webhook spec-confirmed SSRF vectors — needs token to verify internal-IP blocking
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: Swagger UI protected by 401 on real backends; unauthenticated docs are by-design dev portal

## RANKED HYPOTHESES 2026-09-04 09:50:18 UTC
- [82] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,smart-routings,numbers,callforwarding}/{identifier}: IDOR/BOLA on Configuration API tenant-scoped {identifier} CRUD (users, groups, IVRs, queues, smart-routings, numbers, callforwarding) (from art/lead_bigpickle.txt)
- [80] configuration-api.peoplefone.com/customer/voip/v1/{virtualUsers,numbers,users,smart-routings,destinations,callforwarding}/{identifier}: IDOR/BOLA on Configuration API virtualUsers and tenant resources (from art/lead_nemotron3.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Create test account on portal.peoplefone.ch to obtain bearer token; then automated probe of Configuration API /users/{sequential_id} for cross-tenant IDO
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://api.peoplefone.com/services/api-doc/ (read-only, capture full OpenAPI/Swagger JSON spec for SMS, Configuration, and Call Management APIs to e
- LEARN: ACCEPTED IDOR @ configuration-api: Full CRUD on 8 resource types (users, groups, IVRs, queues, numbers, smart-routings, callforwarding, manual-routing) with num
- LEARN: ACCEPTED SSRF @ 5 endpoints: SMS callbackUrl, Smart Routing webhook url, uaCSTA callbackUrl+monitoringCallbackUrl, External Number Lookup webhookUrl — all accep
- LEARN: ACCEPTED BUSLOGIC @ Queue API: agent login/logout actions accept cross-tenant agent+queue identifiers; potential for call center disruption
- LEARN: REJECTED AUTH @ auth.peoplefone.com: Token issuance path NOT in any API spec — must go through portal.peoplefone.ch; auth subdomain standard endpoints return 40
- LEARN: ACCEPTED IDOR @ configuration-api: External Routing API deprecated 2026-09-30 but still live — same webhook SSRF pattern as Smart Routing, may have weaker code 
- LEARN: ACCEPTED IDOR @ configuration-api.peoplefone.com: Multi-tenant API exposes virtualUsers/{identifier} endpoints with explicit authorization boundary notes in spe
- LEARN: ACCEPTED IDOR @ call-api.peoplefone.com: Call control endpoints accept owner.identifier in body with authorization boundary notes
- LEARN: REJECTED MISCONFIG @ www.peoplefone.com: GraphQL introspection hypothesis invalidated — developer portal uses OpenAPI/Swagger, not GraphQL
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: Wildcard DNS dominated by Cloudflare CDN CNAMEs; no dangling third-party targets observed
- LEARN: ACCEPTED IDOR @ api.peoplefone.com: Developer portal explicitly links to public API documentation confirming attack surface
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: Dedicated auth subdomains high-value for session/token flaws
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: wildcard-dominated DNS with all CNAMEs pointing to managed Cloudflare CDN makes dangling CNAME takeover improbable
- LEARN: ACCEPTED IDOR @ api.peoplefone.com: Exposed Swagger UI reveals full SMS/BOLA messageId endpoint surface with per-{messageId} access — high-value BOLA candidate
- LEARN: ACCEPTED SSRF @ api/call-api: Spec-documented attacker-controlled callbackUrl and Smart Routing webhook url constitute server-side-fetch SSRF vectors (post-auth
- LEARN: ACCEPTED IDOR @ configuration-api.peoplefone.com: Newly found tenant-scoped PBX config API (`/customer/voip/v1`) with {identifier} CRUD — IDOR/BOLA candidate
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: Swagger UI is protected by 401 on all real API backends; unauthenticated docs exposure is by-design dev portal, not stand
- LEARN: REJECTED AUTH @ auth.peoplefone.com: Standard OAuth endpoints (/.well-known/oauth-authorization-server, /oauth/authorize) return 404 — authorize endpoint likely
- LEARN: ACCEPTED IDOR @ call-api.peoplefone.com: Call control endpoints accept owner.identifier in body with explicit authorization boundary notes in spec
- LEARN: REJECTED AUTH @ auth.peoplefone.com: Standard OAuth endpoints return 404; authorize endpoint not at standard path; BLOCKED for automation
- LEARN: ACCEPTED IDOR @ configuration-api.peoplefone.com: 235KB spec with explicit authorization boundary notes + {identifier} CRUD — confirmed CRITICAL BOLA candidate
- LEARN: ACCEPTED IDOR @ api.peoplefone.com: SMS messageId endpoint surface confirmed in spec — cross-tenant disclosure viable if tenant isolation absent
- LEARN: ACCEPTED SSRF @ api/call-api: callbackUrl + Smart Routing webhook spec-confirmed SSRF vectors — needs token to verify internal-IP blocking
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: Swagger UI protected by 401 on real backends; unauthenticated docs are by-design dev portal

## RANKED HYPOTHESES 2026-09-04 14:21:14 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: IDOR/BOLA on Configuration API 8 resource types with sequential numeric identifiers (from art/lead_nemotron3.txt)
- [82] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,smart-routings,numbers,callforwarding}/{identifier}: IDOR/BOLA on Configuration API tenant-scoped {identifier} CRUD (users, groups, IVRs, queues, smart-routings, numbers, callforwarding) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Create test account on portal.peoplefone.ch to obtain bearer token; then automated probe of Configuration API /users/{sequential_id} for cross-tenant IDO
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://api.peoplefone.com/services/api-doc/api/ (read-only, capture all 8 OpenAPI YAML specs to extract exact endpoint paths, parameter schemas, aut
- LEARN: ACCEPTED IDOR @ configuration-api: Full CRUD on 8 resource types (users, groups, IVRs, queues, numbers, smart-routings, callforwarding, manual-routing) with num
- LEARN: ACCEPTED SSRF @ 5 endpoints: SMS callbackUrl, Smart Routing webhook url, uaCSTA callbackUrl+monitoringCallbackUrl, External Number Lookup webhookUrl — all accep
- LEARN: ACCEPTED BUSLOGIC @ Queue API: agent login/logout actions accept cross-tenant agent+queue identifiers; potential for call center disruption
- LEARN: REJECTED AUTH @ auth.peoplefone.com: Token issuance path NOT in any API spec — must go through portal.peoplefone.ch; auth subdomain standard endpoints return 40
- LEARN: ACCEPTED IDOR @ configuration-api: External Routing API deprecated 2026-09-30 but still live — same webhook SSRF pattern as Smart Routing, may have weaker code 
- LEARN: ACCEPTED IDOR @ configuration-api.peoplefone.com: Full CRUD on 8 resource types with numeric sequential identifiers; UserResponse exposes sipUserName, physical 
- LEARN: ACCEPTED SSRF @ 5 endpoints: SMS callbackUrl, Smart Routing webhook url, uaCSTA callbackUrl+monitoringCallbackUrl, External Number Lookup webhookUrl — zero host
- LEARN: ACCEPTED BUSLOGIC @ Queue API: agent login/logout accepts cross-tenant agent+queue identifiers; call center disruption
- LEARN: REJECTED AUTH @ auth.peoplefone.com: Token issuance NOT in API specs — requires portal.peoplefone.ch; standard endpoints 404
- LEARN: ACCEPTED IDOR @ configuration-api: External Routing API deprecated 2026-09-30 but live — same SSRF pattern, weaker code paths
- LEARN: ACCEPTED IDOR @ call-api.peoplefone.com: Call control endpoints accept owner.identifier in body with authorization boundary notes
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: Wildcard DNS dominated by Cloudflare CDN CNAMEs; no dangling targets

## RANKED HYPOTHESES 2026-09-04 17:48:47 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: IDOR/BOLA on Configuration API 8 resource types with sequential numeric identifiers (from art/lead_nemotron3.txt)
- NEXT(hypotheses-nemotron3.txt): HUMAN: Create test account on portal.peoplefone.ch to obtain valid bearer token; then automated probe of Configuration API /customer/voip/v1/users/{sequential_i
- LEARN: ACCEPTED IDOR @ configuration-api.peoplefone.com: Full CRUD on 8 resource types with numeric sequential identifiers; UserResponse exposes sipUserName, physical 
- LEARN: ACCEPTED SSRF @ 5 endpoints: SMS callbackUrl, Smart Routing webhook url, uaCSTA callbackUrl+monitoringCallbackUrl, External Number Lookup webhookUrl — zero host
- LEARN: ACCEPTED BUSLOGIC @ Queue API: agent login/logout accepts cross-tenant agent+queue identifiers; call center disruption
- LEARN: REJECTED AUTH @ auth.peoplefone.com: Token issuance NOT in API specs — requires portal.peoplefone.ch; standard endpoints 404
- LEARN: ACCEPTED IDOR @ configuration-api: External Routing API deprecated 2026-09-30 but live — same SSRF pattern, weaker code paths
- LEARN: ACCEPTED IDOR @ call-api.peoplefone.com: Call control endpoints accept owner.identifier in body with authorization boundary notes
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: Wildcard DNS dominated by Cloudflare CDN CNAMEs; no dangling targets

## RANKED HYPOTHESES 2026-09-04 19:59:08 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (from art/lead_nemotron3.txt)
- NEXT(hypotheses-nemotron3.txt): HUMAN: Create test account on portal.peoplefone.ch to obtain valid bearer token; then automated probe of Configuration API /customer/voip/v1/users/{sequential_i
- LEARN: ACCEPTED IDOR @ configuration-api.peoplefone.com: Full CRUD on 8 resource types with numeric sequential identifiers; UserResponse exposes sipUserName, physical 
- LEARN: ACCEPTED SSRF @ 5 endpoints: SMS callbackUrl, Smart Routing webhook url, uaCSTA callbackUrl+monitoringCallbackUrl, External Number Lookup webhookUrl — zero host
- LEARN: ACCEPTED BUSLOGIC @ Queue API: agent login/logout accepts cross-tenant agent+queue identifiers; call center disruption
- LEARN: REJECTED AUTH @ auth.peoplefone.com: Token issuance NOT in API specs — requires portal.peoplefone.ch; standard endpoints 404
- LEARN: ACCEPTED IDOR @ configuration-api: External Routing API deprecated 2026-09-30 but live — same SSRF pattern, weaker code paths
- LEARN: ACCEPTED IDOR @ call-api.peoplefone.com: Call control endpoints accept owner.identifier in body with authorization boundary notes
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: Wildcard DNS dominated by Cloudflare CDN CNAMEs; no dangling targets

## RANKED HYPOTHESES 2026-09-04 22:17:33 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: IDOR/BOLA on Configuration API {identifier} CRUD across 8 resource types (from art/lead_bigpickle.txt)
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (from art/lead_nemotron3.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Within authorized scope, create a test account on portal.peoplefone.ch to obtain a bearer token, then run the two read-only IDOR confirmations (GET /cust
- NEXT(hypotheses-nemotron3.txt): HUMAN: Create test account on portal.peoplefone.ch to obtain valid bearer token; then automated probe of Configuration API /customer/voip/v1/users/{sequential_i
- LEARN: ACCEPTED IDOR @ configuration-api: cross-model convergence (bigpickle+nemotron3) both rank {identifier} CRUD as top candidate; no counter-evidence surfaced — re
- LEARN: ACCEPTED SSRF @ 5 endpoints: no new counter-evidence since spec harvest; retained pending token
- LEARN: ACCEPTED BUSLOGIC @ call-api queue agents: retained at lowest rank — weakest evidence class, spec-silent on membership validation
- LEARN: REJECTED AUTH @ auth.peoplefone.com: re-confirmed token issuance outside all 8 specs and standard endpoints 404 — agent-side token acquisition impossible; human
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: no new dangling-target candidates; wildcard remains Cloudflare CNAME-dominated
- LEARN: ACCEPTED IDOR @ configuration-api.peoplefone.com: Full CRUD on 8 resource types with numeric sequential identifiers; UserResponse exposes sipUserName, physical 
- LEARN: ACCEPTED SSRF @ 5 endpoints: SMS callbackUrl, Smart Routing webhook url, uaCSTA callbackUrl+monitoringCallbackUrl, External Number Lookup webhookUrl — zero host
- LEARN: ACCEPTED BUSLOGIC @ Queue API: agent login/logout accepts cross-tenant agent+queue identifiers; call center disruption
- LEARN: REJECTED AUTH @ auth.peoplefone.com: Token issuance NOT in API specs — requires portal.peoplefone.ch; standard endpoints 404
- LEARN: ACCEPTED IDOR @ configuration-api: External Routing API deprecated 2026-09-30 but live — same SSRF pattern, weaker code paths
- LEARN: ACCEPTED IDOR @ call-api.peoplefone.com: Call control endpoints accept owner.identifier in body with authorization boundary notes
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: Wildcard DNS dominated by Cloudflare CDN CNAMEs; no dangling targets

## RANKED HYPOTHESES 2026-09-05 00:16:08 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (from art/lead_nemotron3.txt)
- [78] auth.peoplefone.com/oauth/authorize: OAuth arbitrary redirect_uri / implicit-token theft on auth service (client_id=1) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: In authorized scope, create a test account via the live self-service `auth.peoplefone.com/de_CH/register` (Turnstile-protected, verified 200), complete t
- NEXT(hypotheses-nemotron3.txt): HUMAN: Create test account on portal.peoplefone.ch to obtain valid bearer token; then automated probe of Configuration API /customer/voip/v1/users/{sequential_i
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: authorize endpoint CONFIRMED LIVE for client_id=1 (302→/de_CH/login preserving arbitrary redirect_uri, implicit+PKCE params
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: oauth/token live (405 on GET) — token-exchange endpoint exists adjacent to unrestricted redirect_uri; final severity turns 
- LEARN: ACCEPTED AUTH @ portal.peoplefone.ch: in-scope customer portal inventoried; Laravel (XSRF-TOKEN + encrypted session cookie); /→/home→/login→auth authorize chain
- LEARN: ACCEPTED OTH @ api.peoplefone.com: swagger-initializer.js lists exactly 8 specs, moving all token/passport/session issuance firmly OFF-spec — OAuth URI flow is 
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — no new dangling-target candidates; wildcard remains Cloudflare CNAME-dominated
- LEARN: ACCEPTED IDOR @ configuration-api.peoplefone.com: Full CRUD on 8 resource types with numeric sequential identifiers; UserResponse exposes sipUserName, physical 
- LEARN: ACCEPTED SSRF @ 5 endpoints: SMS callbackUrl, Smart Routing webhook url, uaCSTA callbackUrl+monitoringCallbackUrl, External Number Lookup webhookUrl — zero host
- LEARN: ACCEPTED BUSLOGIC @ Queue API: agent login/logout accepts cross-tenant agent+queue identifiers; call center disruption
- LEARN: REJECTED AUTH @ auth.peoplefone.com: Token issuance NOT in API specs — requires portal.peoplefone.ch; standard endpoints 404
- LEARN: ACCEPTED IDOR @ configuration-api: External Routing API deprecated 2026-09-30 but live — same SSRF pattern, weaker code paths
- LEARN: ACCEPTED IDOR @ call-api.peoplefone.com: Call control endpoints accept owner.identifier in body with authorization boundary notes
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: Wildcard DNS dominated by Cloudflare CDN CNAMEs; no dangling targets

## RANKED HYPOTHESES 2026-09-05 04:42:31 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (from art/lead_nemotron3.txt)
- NEXT(hypotheses-nemotron3.txt): HUMAN: In authorized scope, create a test account via the live self-service `auth.peoplefone.com/de_CH/register` (Turnstile-protected, verified HTTP 200), compl
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: authorize endpoint CONFIRMED LIVE for client_id=1 (302→/de_CH/login preserving arbitrary redirect_uri, implicit+PKCE params
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: oauth/token live (405 on GET) — token-exchange endpoint exists adjacent to unrestricted redirect_uri; final severity turns 
- LEARN: ACCEPTED AUTH @ portal.peoplefone.ch: in-scope customer portal inventoried; Laravel (XSRF-TOKEN + encrypted session cookie); /→/home→/login→auth authorize chain
- LEARN: ACCEPTED OTH @ api.peoplefone.com: swagger-initializer.js lists exactly 8 specs, moving all token/passport/session issuance firmly OFF-spec — OAuth URI flow is 
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — no new dangling-target candidates; wildcard remains Cloudflare CNAME-dominated
- LEARN: ACCEPTED IDOR @ configuration-api.peoplefone.com: Full CRUD on 8 resource types with numeric sequential identifiers; UserResponse exposes sipUserName, physical 
- LEARN: ACCEPTED SSRF @ 5 endpoints: SMS callbackUrl, Smart Routing webhook url, uaCSTA callbackUrl+monitoringCallbackUrl, External Number Lookup webhookUrl — zero host
- LEARN: ACCEPTED BUSLOGIC @ Queue API: agent login/logout accepts cross-tenant agent+queue identifiers; call center disruption
- LEARN: REJECTED AUTH @ auth.peoplefone.com: Token issuance NOT in API specs — requires portal.peoplefone.ch; standard endpoints 404 (superseded by live authorize disco
- LEARN: ACCEPTED IDOR @ configuration-api: External Routing API deprecated 2026-09-30 but live — same SSRF pattern, weaker code paths
- LEARN: ACCEPTED IDOR @ call-api.peoplefone.com: Call control endpoints accept owner.identifier in body with authorization boundary notes
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: Wildcard DNS dominated by Cloudflare CDN CNAMEs; no dangling targets

## RANKED HYPOTHESES 2026-09-05 08:40:18 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (from art/lead_nemotron3.txt)
- [62] auth.peoplefone.com/oauth/authorize: OAuth client-type / code-theft via unrestricted authorize redirect (client_id=1) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-nemotron3.txt): HUMAN: In authorized scope, create a test account via the live self-service `auth.peoplefone.com/de_CH/register` (Turnstile-protected, verified HTTP 200), compl
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: authorize endpoint CONFIRMED LIVE for client_id=1 (302→/de_CH/login preserving arbitrary redirect_uri, implicit+PKCE params
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: oauth/token live (405 on GET) — token-exchange endpoint exists adjacent to unrestricted redirect_uri; final severity turns 
- LEARN: ACCEPTED AUTH @ portal.peoplefone.ch: in-scope customer portal inventoried; Laravel (XSRF-TOKEN + encrypted session cookie); /→/home→/login→auth authorize chain
- LEARN: ACCEPTED OTH @ api.peoplefone.com: swagger-initializer.js lists exactly 8 specs, moving all token/passport/session issuance firmly OFF-spec — OAuth URI flow is 
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — no new dangling-target candidates; wildcard remains Cloudflare CNAME-dominated
- LEARN: ACCEPTED IDOR @ configuration-api.peoplefone.com: Full CRUD on 8 resource types with numeric sequential identifiers; UserResponse exposes sipUserName, physical 
- LEARN: ACCEPTED SSRF @ 5 endpoints: SMS callbackUrl, Smart Routing webhook url, uaCSTA callbackUrl+monitoringCallbackUrl, External Number Lookup webhookUrl — zero host
- LEARN: ACCEPTED BUSLOGIC @ Queue API: agent login/logout accepts cross-tenant agent+queue identifiers; call center disruption
- LEARN: REJECTED AUTH @ auth.peoplefone.com: Token issuance NOT in API specs — requires portal.peoplefone.ch; standard endpoints 404 (superseded by live authorize disco
- LEARN: ACCEPTED IDOR @ configuration-api: External Routing API deprecated 2026-09-30 but live — same SSRF pattern, weaker code paths
- LEARN: ACCEPTED IDOR @ call-api.peoplefone.com: Call control endpoints accept owner.identifier in body with authorization boundary notes
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: Wildcard DNS dominated by Cloudflare CDN CNAMEs; no dangling targets

## RANKED HYPOTHESES 2026-09-05 12:06:02 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (from art/lead_nemotron3.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: The triage (12:00) confirmed OAuth redirect_uri as the single report-ready finding (VALID 9.1 CRITICAL-conditional). Two competing tracks: (a) REPORT the
- NEXT(hypotheses-nemotron3.txt): HUMAN: In authorized scope, create a test account via the live self-service `auth.peoplefone.com/de_CH/register` (Turnstile-protected, verified HTTP 200), compl
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: re-confirmed authorize is stateless-404 in a fresh session (my 08:40-era probe) — 302 preserving attacker redirect_uri only
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage 12:00 formally INVALID (spec-silent on membership validation); drop from priority.
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: authorize endpoint CONFIRMED LIVE for client_id=1 (302→/de_CH/login preserving arbitrary redirect_uri, implicit+PKCE params
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: oauth/token live (405 on GET) — token-exchange endpoint exists adjacent to unrestricted redirect_uri; final severity turns 
- LEARN: ACCEPTED AUTH @ portal.peoplefone.ch: in-scope customer portal inventoried; Laravel (XSRF-TOKEN + encrypted session cookie); /→/home→/login→auth authorize chain
- LEARN: ACCEPTED OTH @ api.peoplefone.com: swagger-initializer.js lists exactly 8 specs, moving all token/passport/session issuance firmly OFF-spec — OAuth URI flow is 
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — no new dangling-target candidates; wildcard remains Cloudflare CNAME-dominated
- LEARN: ACCEPTED IDOR @ configuration-api.peoplefone.com: Full CRUD on 8 resource types with numeric sequential identifiers; UserResponse exposes sipUserName, physical 
- LEARN: ACCEPTED SSRF @ 5 endpoints: SMS callbackUrl, Smart Routing webhook url, uaCSTA callbackUrl+monitoringCallbackUrl, External Number Lookup webhookUrl — zero host
- LEARN: ACCEPTED BUSLOGIC @ Queue API: agent login/logout accepts cross-tenant agent+queue identifiers; call center disruption
- LEARN: REJECTED AUTH @ auth.peoplefone.com: Token issuance NOT in API specs — requires portal.peoplefone.ch; standard endpoints 404 (superseded by live authorize disco
- LEARN: ACCEPTED IDOR @ configuration-api: External Routing API deprecated 2026-09-30 but live — same SSRF pattern, weaker code paths
- LEARN: ACCEPTED IDOR @ call-api.peoplefone.com: Call control endpoints accept owner.identifier in body with authorization boundary notes
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: Wildcard DNS dominated by Cloudflare CDN CNAMEs; no dangling targets

## RANKED HYPOTHESES 2026-09-05 15:27:47 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (8 resource types) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Submit the OAuth open-redirect/redirect_uri finding to bugs.olivermaicher.eu now — triage 12:00 graded VALID 9.1 CRITICAL-conditional; include the 302 tr
- NEXT(hypotheses-nemotron3.txt): HUMAN: In authorized scope, create a test account via the live self-service `auth.peoplefone.com/de_CH/register` (Turnstile-protected, previously HTTP 200, curr
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: live re-probe frozen state — oauth/token 405 (live), stateless authorize 404 (fresh session), register 500 (regression hold
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage 12:00 formal INVALID (spec-silent on membership validation); removed from active set — no re-probe warranted.
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence since spec harvest; cross-model rank holds — retains top slot, remains token-gated.
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: authorize endpoint CONFIRMED LIVE for client_id=1 (302→/de_CH/login preserving arbitrary redirect_uri, implicit+PKCE params
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: oauth/token live (405 on GET) — token-exchange endpoint exists adjacent to unrestricted redirect_uri; final severity turns 
- LEARN: ACCEPTED AUTH @ portal.peoplefone.ch: in-scope customer portal inventoried; Laravel (XSRF-TOKEN + encrypted session cookie); /→/home→/login→auth authorize chain
- LEARN: ACCEPTED OTH @ api.peoplefone.com: swagger-initializer.js lists exactly 8 specs, moving all token/passport/session issuance firmly OFF-spec — OAuth URI flow is 
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — no new dangling-target candidates; wildcard remains Cloudflare CNAME-dominated
- LEARN: ACCEPTED IDOR @ configuration-api.peoplefone.com: Full CRUD on 8 resource types with numeric sequential identifiers; UserResponse exposes sipUserName, physical 
- LEARN: ACCEPTED SSRF @ 5 endpoints: SMS callbackUrl, Smart Routing webhook url, uaCSTA callbackUrl+monitoringCallbackUrl, External Number Lookup webhookUrl — zero host
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage 12:00 formally INVALID (spec-silent on membership validation); drop from priority
- LEARN: ACCEPTED IDOR @ configuration-api: External Routing API deprecated 2026-09-30 but live — same SSRF pattern, weaker code paths
- LEARN: ACCEPTED IDOR @ call-api.peoplefone.com: Call control endpoints accept owner.identifier in body with authorization boundary notes
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: Wildcard DNS dominated by Cloudflare CDN CNAMEs; no dangling targets

## RANKED HYPOTHESES 2026-09-05 17:42:47 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (8 resource types) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Submit the OAuth open-redirect/redirect_uri finding to bugs.olivermaicher.eu now — triage 12:00 graded VALID 9.1 CRITICAL-conditional; include the 302 tr
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/redirect_uri finding to bugs.olivermaicher.eu now — triage 12:00 graded VALID 9.1 CRITICAL-conditional; include the 302 tr
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: live re-probe frozen state — oauth/token 405 (live), stateless authorize 404 (fresh session), register 500 (regression hold
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage 12:00 formal INVALID (spec-silent on membership validation); removed from active set — no re-probe warranted.
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence since spec harvest; cross-model rank holds — retains top slot, remains token-gated.
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: authorize endpoint CONFIRMED LIVE for client_id=1 (302→/de_CH/login preserving arbitrary redirect_uri, implicit+PKCE params
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: oauth/token live (405 on GET) — token-exchange endpoint exists adjacent to unrestricted redirect_uri; final severity turns 
- LEARN: ACCEPTED AUTH @ portal.peoplefone.ch: in-scope customer portal inventoried; Laravel (XSRF-TOKEN + encrypted session cookie); /→/home→/login→auth authorize chain
- LEARN: ACCEPTED OTH @ api.peoplefone.com: swagger-initializer.js lists exactly 8 specs, moving all token/passport/session issuance firmly OFF-spec — OAuth URI flow is 
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — no new dangling-target candidates; wildcard remains Cloudflare CNAME-dominated
- LEARN: ACCEPTED IDOR @ configuration-api.peoplefone.com: Full CRUD on 8 resource types with numeric sequential identifiers; UserResponse exposes sipUserName, physical 
- LEARN: ACCEPTED SSRF @ 5 endpoints: SMS callbackUrl, Smart Routing webhook url, uaCSTA callbackUrl+monitoringCallbackUrl, External Number Lookup webhookUrl — zero host
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage 12:00 formally INVALID (spec-silent on membership validation); drop from priority
- LEARN: ACCEPTED IDOR @ configuration-api: External Routing API deprecated 2026-09-30 but live — same SSRF pattern, weaker code paths
- LEARN: ACCEPTED IDOR @ call-api.peoplefone.com: Call control endpoints accept owner.identifier in body with authorization boundary notes
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: Wildcard DNS dominated by Cloudflare CDN CNAMEs; no dangling targets

## RANKED HYPOTHESES 2026-09-05 19:35:12 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (8 resource types) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Submit the OAuth open-redirect/redirect_uri finding to bugs.olivermaicher.eu now — triage 12:00 graded VALID 9.1 CRITICAL-conditional; include the 302 tr
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/redirect_uri finding to bugs.olivermaicher.eu now — triage 12:00 graded VALID 9.1 CRITICAL-conditional; include the 302 tr
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: live re-probe frozen state — oauth/token 405 (live), stateless authorize 404 (fresh session), register 500 (regression hold
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage 12:00 formal INVALID (spec-silent on membership validation); removed from active set — no re-probe warranted.
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence since spec harvest; cross-model rank holds — retains top slot, remains token-gated.
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: this cycle NO_DELTA — state frozen at oauth/token 405 / stateless authorize 404 / register 500; consistent with 12:00 triag
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: still no counter-evidence; cross-model rank holds — retains top slot, remains token-gated.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence this cycle; retained pending token.
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: authorize endpoint CONFIRMED LIVE for client_id=1 (302→/de_CH/login preserving arbitrary redirect_uri, implicit+PKCE params
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: oauth/token live (405 on GET) — token-exchange endpoint exists adjacent to unrestricted redirect_uri; final severity turns 
- LEARN: ACCEPTED AUTH @ portal.peoplefone.ch: in-scope customer portal inventoried; Laravel (XSRF-TOKEN + encrypted session cookie); /→/home→/login→auth authorize chain
- LEARN: ACCEPTED OTH @ api.peoplefone.com: swagger-initializer.js lists exactly 8 specs, moving all token/passport/session issuance firmly OFF-spec — OAuth URI flow is 
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — no new dangling-target candidates; wildcard remains Cloudflare CNAME-dominated
- LEARN: ACCEPTED IDOR @ configuration-api.peoplefone.com: Full CRUD on 8 resource types with numeric sequential identifiers; UserResponse exposes sipUserName, physical 
- LEARN: ACCEPTED SSRF @ 5 endpoints: SMS callbackUrl, Smart Routing webhook url, uaCSTA callbackUrl+monitoringCallbackUrl, External Number Lookup webhookUrl — zero host
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage 12:00 formally INVALID (spec-silent on membership validation); drop from priority
- LEARN: ACCEPTED IDOR @ configuration-api: External Routing API deprecated 2026-09-30 but live — same SSRF pattern, weaker code paths
- LEARN: ACCEPTED IDOR @ call-api.peoplefone.com: Call control endpoints accept owner.identifier in body with authorization boundary notes
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: Wildcard DNS dominated by Cloudflare CDN CNAMEs; no dangling targets

## RANKED HYPOTHESES 2026-09-05 21:46:33 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (8 resource types) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/redirect_uri finding to bugs.olivermaicher.eu now — triage 12:00 graded VALID 9.1 CRITICAL-conditional; include the 302 tr
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: authorize endpoint CONFIRMED LIVE for client_id=1 (302→/de_CH/login preserving arbitrary redirect_uri, implicit+PKCE params
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: oauth/token live (405 on GET) — token-exchange endpoint exists adjacent to unrestricted redirect_uri; final severity turns 
- LEARN: ACCEPTED AUTH @ portal.peoplefone.ch: in-scope customer portal inventoried; Laravel (XSRF-TOKEN + encrypted session cookie); /→/home→/login→auth authorize chain
- LEARN: ACCEPTED OTH @ api.peoplefone.com: swagger-initializer.js lists exactly 8 specs, moving all token/passport/session issuance firmly OFF-spec — OAuth URI flow is 
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — no new dangling-target candidates; wildcard remains Cloudflare CNAME-dominated
- LEARN: ACCEPTED IDOR @ configuration-api.peoplefone.com: Full CRUD on 8 resource types with numeric sequential identifiers; UserResponse exposes sipUserName, physical 
- LEARN: ACCEPTED SSRF @ 5 endpoints: SMS callbackUrl, Smart Routing webhook url, uaCSTA callbackUrl+monitoringCallbackUrl, External Number Lookup webhookUrl — zero host
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage 12:00 formally INVALID (spec-silent on membership validation); drop from priority
- LEARN: ACCEPTED IDOR @ configuration-api: External Routing API deprecated 2026-09-30 but live — same SSRF pattern, weaker code paths
- LEARN: ACCEPTED IDOR @ call-api.peoplefone.com: Call control endpoints accept owner.identifier in body with authorization boundary notes
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: Wildcard DNS dominated by Cloudflare CDN CNAMEs; no dangling targets

## RANKED HYPOTHESES 2026-09-05 23:39:47 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (8 resource types) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Submit the OAuth redirect_uri/open-redirect finding to bugs.olivermaicher.eu (triage 12:00 VALID 9.1 CRITICAL-conditional) — package today's stability da
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/redirect_uri finding to bugs.olivermaicher.eu now — triage 12:00 graded VALID 9.1 CRITICAL-conditional; include the 302 tr
- LEARN: ACCEPTED @ auth.peoplefone.com: NO_DELTA state frozen at register 500 / token 405 / stateless authorize 404; portal 302 and api-doc 200 baseline — consistent wi
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence this cycle; rank holds; token-gated.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence this cycle; retained pending token.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — wildcard remains Cloudflare CNAME-dominated; no new dangling targets.
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: authorize endpoint CONFIRMED LIVE for client_id=1 (302→/de_CH/login preserving arbitrary redirect_uri, implicit+PKCE params
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: oauth/token live (405 on GET) — token-exchange endpoint exists adjacent to unrestricted redirect_uri; final severity turns 
- LEARN: ACCEPTED AUTH @ portal.peoplefone.ch: in-scope customer portal inventoried; Laravel (XSRF-TOKEN + encrypted session cookie); /→/home→/login→auth authorize chain
- LEARN: ACCEPTED OTH @ api.peoplefone.com: swagger-initializer.js lists exactly 8 specs, moving all token/passport/session issuance firmly OFF-spec — OAuth URI flow is 
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — no new dangling-target candidates; wildcard remains Cloudflare CNAME-dominated
- LEARN: ACCEPTED IDOR @ configuration-api.peoplefone.com: Full CRUD on 8 resource types with numeric sequential identifiers; UserResponse exposes sipUserName, physical 
- LEARN: ACCEPTED SSRF @ 5 endpoints: SMS callbackUrl, Smart Routing webhook url, uaCSTA callbackUrl+monitoringCallbackUrl, External Number Lookup webhookUrl — zero host
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage 12:00 formally INVALID (spec-silent on membership validation); drop from priority
- LEARN: ACCEPTED IDOR @ configuration-api: External Routing API deprecated 2026-09-30 but live — same SSRF pattern, weaker code paths
- LEARN: ACCEPTED IDOR @ call-api.peoplefone.com: Call control endpoints accept owner.identifier in body with authorization boundary notes
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: Wildcard DNS dominated by Cloudflare CDN CNAMEs; no dangling targets

## RANKED HYPOTHESES 2026-09-06 01:23:13 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (8 resource types) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Submit the OAuth redirect_uri/open-redirect finding to bugs.olivermaicher.eu (triage 12:00 VALID 9.1 CRITICAL-conditional) — package today's stability da
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/redirect_uri finding to bugs.olivermaicher.eu now — triage 12:00 graded VALID 9.1 CRITICAL-conditional; include the 302 tr
- LEARN: ACCEPTED @ auth.peoplefone.com: NO_DELTA state frozen at register 500 / token 405 / stateless authorize 404; portal 302 and api-doc 200 baseline — consistent wi
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence this cycle; rank holds; token-gated.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence this cycle; retained pending token.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — wildcard remains Cloudflare CNAME-dominated; no new dangling targets.
- LEARN: ACCEPTED @ auth.peoplefone.com: NO_DELTA state frozen at register 500 / token 405 / stateless authorize 404; portal 302 and api-doc 200 baseline — consistent wi
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence this cycle; rank holds; token-gated.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence this cycle; retained pending token.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — wildcard remains Cloudflare CNAME-dominated; no new dangling targets.
- LEARN: ACCEPTED @ auth.peoplefone.com: NO_DELTA — register 500 / token 405 / stateless authorize 404 / portal 302 / api-doc 200 verified fresh; consistent with 12:00 a
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (9th frozen cycle).
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — wildcard remains Cloudflare CNAME-dominated; reposcan no alternative surface.
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: authorize endpoint CONFIRMED LIVE for client_id=1 (302→/de_CH/login preserving arbitrary redirect_uri, implicit+PKCE params
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: oauth/token live (405 on GET) — token-exchange endpoint exists adjacent to unrestricted redirect_uri; final severity turns 
- LEARN: ACCEPTED AUTH @ portal.peoplefone.ch: in-scope customer portal inventoried; Laravel (XSRF-TOKEN + encrypted session cookie); /→/home→/login→auth authorize chain
- LEARN: ACCEPTED OTH @ api.peoplefone.com: swagger-initializer.js lists exactly 8 specs, moving all token/passport/session issuance firmly OFF-spec — OAuth URI flow is 
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — no new dangling-target candidates; wildcard remains Cloudflare CNAME-dominated
- LEARN: ACCEPTED IDOR @ configuration-api.peoplefone.com: Full CRUD on 8 resource types with numeric sequential identifiers; UserResponse exposes sipUserName, physical 
- LEARN: ACCEPTED SSRF @ 5 endpoints: SMS callbackUrl, Smart Routing webhook url, uaCSTA callbackUrl+monitoringCallbackUrl, External Number Lookup webhookUrl — zero host
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage 12:00 formally INVALID (spec-silent on membership validation); drop from priority
- LEARN: ACCEPTED IDOR @ configuration-api: External Routing API deprecated 2026-09-30 but live — same SSRF pattern, weaker code paths
- LEARN: ACCEPTED IDOR @ call-api.peoplefone.com: Call control endpoints accept owner.identifier in body with authorization boundary notes
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: Wildcard DNS dominated by Cloudflare CDN CNAMEs; no dangling targets

## RANKED HYPOTHESES 2026-09-06 06:31:53 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (from art/lead_nemotron3.txt)
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/redirect_uri finding to bugs.olivermaicher.eu now — triage 12:00 graded VALID 9.1 CRITICAL-conditional; include the 302 tr
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: authorize endpoint CONFIRMED LIVE for client_id=1 (302→/de_CH/login preserving arbitrary redirect_uri, implicit+PKCE params
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: oauth/token live (405 on GET) — token-exchange endpoint exists adjacent to unrestricted redirect_uri; final severity turns 
- LEARN: ACCEPTED AUTH @ portal.peoplefone.ch: in-scope customer portal inventoried; Laravel (XSRF-TOKEN + encrypted session cookie); /→/home→/login→auth authorize chain
- LEARN: ACCEPTED OTH @ api.peoplefone.com: swagger-initializer.js lists exactly 8 specs, moving all token/passport/session issuance firmly OFF-spec — OAuth URI flow is 
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — no new dangling-target candidates; wildcard remains Cloudflare CNAME-dominated
- LEARN: ACCEPTED IDOR @ configuration-api.peoplefone.com: Full CRUD on 8 resource types with numeric sequential identifiers; UserResponse exposes sipUserName, physical 
- LEARN: ACCEPTED SSRF @ 5 endpoints: SMS callbackUrl, Smart Routing webhook url, uaCSTA callbackUrl+monitoringCallbackUrl, External Number Lookup webhookUrl — zero host
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage 12:00 formally INVALID (spec-silent on membership validation); drop from priority
- LEARN: ACCEPTED IDOR @ configuration-api: External Routing API deprecated 2026-09-30 but live — same SSRF pattern, weaker code paths
- LEARN: ACCEPTED IDOR @ call-api.peoplefone.com: Call control endpoints accept owner.identifier in body with authorization boundary notes
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: Wildcard DNS dominated by Cloudflare CDN CNAMEs; no dangling targets

## RANKED HYPOTHESES 2026-09-06 11:29:47 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (8 resource types) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Submit the OAuth redirect_uri/open-redirect finding to bugs.olivermaicher.eu now — triage VALID 9.1 CRITICAL-conditional across three independent triage 
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/redirect_uri finding to bugs.olivermaicher.eu now — triage 12:00 graded VALID 9.1 CRITICAL-conditional; include the 302 tr
- LEARN: ACCEPTED @ auth.peoplefone.com: NO_DELTA re-verified live — api-doc 200 / oauth/token 405 / register 500; consistent with 12:00 and 00:15 triage; no new surface
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (10th frozen cycle).
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — wildcard remains Cloudflare CNAME-dominated; no new dangling targets; reposcan yields no alternative surface.
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: authorize endpoint CONFIRMED LIVE for client_id=1 (302→/de_CH/login preserving arbitrary redirect_uri, implicit+PKCE params
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: oauth/token live (405 on GET) — token-exchange endpoint exists adjacent to unrestricted redirect_uri; final severity turns 
- LEARN: ACCEPTED AUTH @ portal.peoplefone.ch: in-scope customer portal inventoried; Laravel (XSRF-TOKEN + encrypted session cookie); /→/home→/login→auth authorize chain
- LEARN: ACCEPTED OTH @ api.peoplefone.com: swagger-initializer.js lists exactly 8 specs, moving all token/passport/session issuance firmly OFF-spec — OAuth URI flow is 
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — no new dangling-target candidates; wildcard remains Cloudflare CNAME-dominated
- LEARN: ACCEPTED IDOR @ configuration-api.peoplefone.com: Full CRUD on 8 resource types with numeric sequential identifiers; UserResponse exposes sipUserName, physical 
- LEARN: ACCEPTED SSRF @ 5 endpoints: SMS callbackUrl, Smart Routing webhook url, uaCSTA callbackUrl+monitoringCallbackUrl, External Number Lookup webhookUrl — zero host
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage 12:00 formally INVALID (spec-silent on membership validation); drop from priority
- LEARN: ACCEPTED IDOR @ configuration-api: External Routing API deprecated 2026-09-30 but live — same SSRF pattern, weaker code paths
- LEARN: ACCEPTED IDOR @ call-api.peoplefone.com: Call control endpoints accept owner.identifier in body with authorization boundary notes
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: Wildcard DNS dominated by Cloudflare CDN CNAMEs; no dangling targets

## RANKED HYPOTHESES 2026-09-06 14:26:37 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (from art/lead_nemotron3.txt)
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/redirect_uri finding to bugs.olivermaicher.eu now — triage 12:00 graded VALID 9.1 CRITICAL-conditional; include the 302 tr
- LEARN: ACCEPTED @ auth.peoplefone.com: NO_DELTA re-verified live — api-doc 200 / oauth/token 405 / register 500; consistent with 12:00 and 00:15 triage; no new surface
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (11th frozen cycle).
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — wildcard remains Cloudflare CNAME-dominated; no new dangling targets; reposcan yields no alternative surface.
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage 00:15 formally INVALID (spec-silent on membership validation); removed from active set.
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: authorize endpoint CONFIRMED LIVE for client_id=1 (302→/de_CH/login preserving arbitrary redirect_uri, implicit+PKCE params
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: oauth/token live (405 on GET) — token-exchange endpoint exists adjacent to unrestricted redirect_uri; final severity turns 
- LEARN: ACCEPTED AUTH @ portal.peoplefone.ch: in-scope customer portal inventoried; Laravel (XSRF-TOKEN + encrypted session cookie); /→/home→/login→auth authorize chain
- LEARN: ACCEPTED OTH @ api.peoplefone.com: swagger-initializer.js lists exactly 8 specs, moving all token/passport/session issuance firmly OFF-spec — OAuth URI flow is 
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — no new dangling-target candidates; wildcard remains Cloudflare CNAME-dominated
- LEARN: ACCEPTED IDOR @ configuration-api.peoplefone.com: Full CRUD on 8 resource types with numeric sequential identifiers; UserResponse exposes sipUserName, physical 
- LEARN: ACCEPTED SSRF @ 5 endpoints: SMS callbackUrl, Smart Routing webhook url, uaCSTA callbackUrl+monitoringCallbackUrl, External Number Lookup webhookUrl — zero host
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage 12:00 formally INVALID (spec-silent on membership validation); drop from priority
- LEARN: ACCEPTED IDOR @ configuration-api: External Routing API deprecated 2026-09-30 but live — same SSRF pattern, weaker code paths
- LEARN: ACCEPTED IDOR @ call-api.peoplefone.com: Call control endpoints accept owner.identifier in body with authorization boundary notes
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: Wildcard DNS dominated by Cloudflare CDN CNAMEs; no dangling targets

## RANKED HYPOTHESES 2026-09-06 17:11:44 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (from art/lead_nemotron3.txt)
- [62] auth.peoplefone.com/oauth/authorize: OAuth arbitrary redirect_uri / code-theft (client_id=1) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Submit the OAuth redirect_uri/open-redirect finding to bugs.olivermaicher.eu now — triage VALID 9.1 CRITICAL-conditional across three independent triage 
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/redirect_uri finding to bugs.olivermaicher.eu now — triage 12:00 graded VALID 9.1 CRITICAL-conditional; include the 302 tr
- LEARN: ACCEPTED @ auth.peoplefone.com: NO_DELTA re-verified live — api-doc 200 / oauth/token 405 / register 500; consistent with 12:00 and 00:15 triage; no new surface
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (11th frozen cycle).
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — wildcard remains Cloudflare CNAME-dominated; no new dangling targets; reposcan yields no alternative surface.
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage 00:15 formally INVALID (spec-silent on membership validation); removed from active set.
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: authorize endpoint CONFIRMED LIVE for client_id=1 (302→/de_CH/login preserving arbitrary redirect_uri, implicit+PKCE params
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: oauth/token live (405 on GET) — token-exchange endpoint exists adjacent to unrestricted redirect_uri; final severity turns 
- LEARN: ACCEPTED AUTH @ portal.peoplefone.ch: in-scope customer portal inventoried; Laravel (XSRF-TOKEN + encrypted session cookie); /→/home→/login→auth authorize chain
- LEARN: ACCEPTED OTH @ api.peoplefone.com: swagger-initializer.js lists exactly 8 specs, moving all token/passport/session issuance firmly OFF-spec — OAuth URI flow is 
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — no new dangling-target candidates; wildcard remains Cloudflare CNAME-dominated
- LEARN: ACCEPTED IDOR @ configuration-api.peoplefone.com: Full CRUD on 8 resource types with numeric sequential identifiers; UserResponse exposes sipUserName, physical 
- LEARN: ACCEPTED SSRF @ 5 endpoints: SMS callbackUrl, Smart Routing webhook url, uaCSTA callbackUrl+monitoringCallbackUrl, External Number Lookup webhookUrl — zero host
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage 12:00 formally INVALID (spec-silent on membership validation); drop from priority
- LEARN: ACCEPTED IDOR @ configuration-api: External Routing API deprecated 2026-09-30 but live — same SSRF pattern, weaker code paths
- LEARN: ACCEPTED IDOR @ call-api.peoplefone.com: Call control endpoints accept owner.identifier in body with authorization boundary notes
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: Wildcard DNS dominated by Cloudflare CDN CNAMEs; no dangling targets

## RANKED HYPOTHESES 2026-09-06 19:31:05 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (from art/lead_nemotron3.txt)
- [62] auth.peoplefone.com/oauth/authorize: OAuth arbitrary redirect_uri / code-theft (client_id=1) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Submit the OAuth redirect_uri/open-redirect finding to bugs.olivermaicher.eu now — triage VALID 9.1 CRITICAL-conditional across three independent triage 
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/redirect_uri finding to bugs.olivermaicher.eu now — triage 12:00 graded VALID 9.1 CRITICAL-conditional; include the 302 tr
- LEARN: ACCEPTED @ auth.peoplefone.com: NO_DELTA re-verified live — api-doc 200 / oauth/token 405 / register 500; consistent with 12:00 and 00:15 triage; no new surface
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (11th frozen cycle).
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — wildcard remains Cloudflare CNAME-dominated; no new dangling targets; reposcan yields no alternative surface.
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage 00:15 formally INVALID (spec-silent on membership validation); removed from active set.
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: authorize endpoint CONFIRMED LIVE for client_id=1 (302→/de_CH/login preserving arbitrary redirect_uri, implicit+PKCE params
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: oauth/token live (405 on GET) — token-exchange endpoint exists adjacent to unrestricted redirect_uri; final severity turns 
- LEARN: ACCEPTED AUTH @ portal.peoplefone.ch: in-scope customer portal inventoried; Laravel (XSRF-TOKEN + encrypted session cookie); /→/home→/login→auth authorize chain
- LEARN: ACCEPTED OTH @ api.peoplefone.com: swagger-initializer.js lists exactly 8 specs, moving all token/passport/session issuance firmly OFF-spec — OAuth URI flow is 
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — no new dangling-target candidates; wildcard remains Cloudflare CNAME-dominated
- LEARN: ACCEPTED IDOR @ configuration-api.peoplefone.com: Full CRUD on 8 resource types with numeric sequential identifiers; UserResponse exposes sipUserName, physical 
- LEARN: ACCEPTED SSRF @ 5 endpoints: SMS callbackUrl, Smart Routing webhook url, uaCSTA callbackUrl+monitoringCallbackUrl, External Number Lookup webhookUrl — zero host
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage 12:00 formally INVALID (spec-silent on membership validation); drop from priority
- LEARN: ACCEPTED IDOR @ configuration-api: External Routing API deprecated 2026-09-30 but live — same SSRF pattern, weaker code paths
- LEARN: ACCEPTED IDOR @ call-api.peoplefone.com: Call control endpoints accept owner.identifier in body with authorization boundary notes
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: Wildcard DNS dominated by Cloudflare CDN CNAMEs; no dangling targets

## RANKED HYPOTHESES 2026-09-06 21:30:15 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (from art/lead_nemotron3.txt)
- [62] auth.peoplefone.com/oauth/authorize: OAuth arbitrary redirect_uri / code-theft (client_id=1) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/redirect_uri finding to bugs.olivermaicher.eu now — triage 12:00 graded VALID 9.1 CRITICAL-conditional; include the 302 tr
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: authorize endpoint CONFIRMED LIVE for client_id=1 (302→/de_CH/login preserving arbitrary redirect_uri, implicit+PKCE params
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: oauth/token live (405 on GET) — token-exchange endpoint exists adjacent to unrestricted redirect_uri; final severity turns 
- LEARN: ACCEPTED AUTH @ portal.peoplefone.ch: in-scope customer portal inventoried; Laravel (XSRF-TOKEN + encrypted session cookie); /→/home→/login→auth authorize chain
- LEARN: ACCEPTED OTH @ api.peoplefone.com: swagger-initializer.js lists exactly 8 specs, moving all token/passport/session issuance firmly OFF-spec — OAuth URI flow is 
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — no new dangling-target candidates; wildcard remains Cloudflare CNAME-dominated
- LEARN: ACCEPTED IDOR @ configuration-api.peoplefone.com: Full CRUD on 8 resource types with numeric sequential identifiers; UserResponse exposes sipUserName, physical 
- LEARN: ACCEPTED SSRF @ 5 endpoints: SMS callbackUrl, Smart Routing webhook url, uaCSTA callbackUrl+monitoringCallbackUrl, External Number Lookup webhookUrl — zero host
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage 12:00 formally INVALID (spec-silent on membership validation); drop from priority
- LEARN: ACCEPTED IDOR @ configuration-api: External Routing API deprecated 2026-09-30 but live — same SSRF pattern, weaker code paths
- LEARN: ACCEPTED IDOR @ call-api.peoplefone.com: Call control endpoints accept owner.identifier in body with authorization boundary notes
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: Wildcard DNS dominated by Cloudflare CDN CNAMEs; no dangling targets

## RANKED HYPOTHESES 2026-09-06 23:10:54 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (from art/lead_nemotron3.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Submit the OAuth redirect_uri/open-redirect finding to bugs.olivermaicher.eu now — triage VALID 9.1 CRITICAL-conditional across three independent runs. P
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/redirect_uri finding to bugs.olivermaicher.eu now — triage 12:00 graded VALID 9.1 CRITICAL-conditional; include the 302 tr
- LEARN: ACCEPTED @ auth.peoplefone.com: NO_DELTA re-verified live this cycle via fresh client_id=1 probes (api-doc 200 / oauth/token 405 / register 500 / stateless auth
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (13th frozen cycle).
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — wildcard remains Cloudflare CNAME-dominated; no new dangling targets; reposcan yields no alternative surface.
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage-formal INVALID (spec-silent on membership validation); removed from active set.
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: authorize endpoint CONFIRMED LIVE for client_id=1 (302→/de_CH/login preserving arbitrary redirect_uri, implicit+PKCE params
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: oauth/token live (405 on GET) — token-exchange endpoint exists adjacent to unrestricted redirect_uri; final severity turns 
- LEARN: ACCEPTED AUTH @ portal.peoplefone.ch: in-scope customer portal inventoried; Laravel (XSRF-TOKEN + encrypted session cookie); /→/home→/login→auth authorize chain
- LEARN: ACCEPTED OTH @ api.peoplefone.com: swagger-initializer.js lists exactly 8 specs, moving all token/passport/session issuance firmly OFF-spec — OAuth URI flow is 
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — no new dangling-target candidates; wildcard remains Cloudflare CNAME-dominated
- LEARN: ACCEPTED IDOR @ configuration-api.peoplefone.com: Full CRUD on 8 resource types with numeric sequential identifiers; UserResponse exposes sipUserName, physical 
- LEARN: ACCEPTED SSRF @ 5 endpoints: SMS callbackUrl, Smart Routing webhook url, uaCSTA callbackUrl+monitoringCallbackUrl, External Number Lookup webhookUrl — zero host
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage 12:00 formally INVALID (spec-silent on membership validation); drop from priority
- LEARN: ACCEPTED IDOR @ configuration-api: External Routing API deprecated 2026-09-30 but live — same SSRF pattern, weaker code paths
- LEARN: ACCEPTED IDOR @ call-api.peoplefone.com: Call control endpoints accept owner.identifier in body with authorization boundary notes
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: Wildcard DNS dominated by Cloudflare CDN CNAMEs; no dangling targets

## RANKED HYPOTHESES 2026-09-07 01:12:39 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (from art/lead_nemotron3.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Immediately report the guaranteed primitive to bugs.olivermaicher.eu — OAuth authorize open-redirect/login-CSRF (arbitrary redirect_uri preserved 302→/de
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/redirect_uri finding to bugs.olivermaicher.eu now — triage 12:00 graded VALID 9.1 CRITICAL-conditional; include the 302 tr
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: NEW — POST oauth/token with no client_secret → invalid_client JSON for clients 1/4/5 (confidential); nonexistent ids 2,3,10
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: NEW — 11 guessed subdomains (admin/mail/staging/test/dev-api/status/shop/billing/webmail/crm/pbx/voip) all NXDOMAIN → NO 
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (14th frozen cycle).
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token.
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: authorize endpoint CONFIRMED LIVE for client_id=1 (302→/de_CH/login preserving arbitrary redirect_uri, implicit+PKCE params
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: oauth/token live (405 on GET) — token-exchange endpoint exists adjacent to unrestricted redirect_uri; final severity turns 
- LEARN: ACCEPTED AUTH @ portal.peoplefone.ch: in-scope customer portal inventoried; Laravel (XSRF-TOKEN + encrypted session cookie); /→/home→/login→auth authorize chain
- LEARN: ACCEPTED OTH @ api.peoplefone.com: swagger-initializer.js lists exactly 8 specs, moving all token/passport/session issuance firmly OFF-spec — OAuth URI flow is 
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — no new dangling-target candidates; wildcard remains Cloudflare CNAME-dominated
- LEARN: ACCEPTED IDOR @ configuration-api.peoplefone.com: Full CRUD on 8 resource types with numeric sequential identifiers; UserResponse exposes sipUserName, physical 
- LEARN: ACCEPTED SSRF @ 5 endpoints: SMS callbackUrl, Smart Routing webhook url, uaCSTA callbackUrl+monitoringCallbackUrl, External Number Lookup webhookUrl — zero host
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage 12:00 formally INVALID (spec-silent on membership validation); drop from priority
- LEARN: ACCEPTED IDOR @ configuration-api: External Routing API deprecated 2026-09-30 but live — same SSRF pattern, weaker code paths
- LEARN: ACCEPTED IDOR @ call-api.peoplefone.com: Call control endpoints accept owner.identifier in body with authorization boundary notes
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: Wildcard DNS dominated by Cloudflare CDN CNAMEs; no dangling targets

## RANKED HYPOTHESES 2026-09-07 06:14:29 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (8 resource types) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding (arbitrary redirect_uri preserved 302→/de_CH/login for client_id=1, implicit+PKCE accepted when portal-
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/redirect_uri finding to bugs.olivermaicher.eu now — triage 12:00 graded VALID 9.1 CRITICAL-conditional; include the 302 tr
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: NO_DELTA re-verified live this cycle (token 401 invalid_client known clients / 500 nonexistent, register 500, stateless aut
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (15th frozen cycle).
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — 11 guessed subdomains all NXDOMAIN (NO wildcard), no dangling CNAME targets; reposcan yields no alternative s
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage-formal INVALID (spec-silent on membership validation); removed from active set.
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: NEW — POST oauth/token with no client_secret → invalid_client JSON for clients 1/4/5 (confidential); nonexistent ids 2,3,10
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: NEW — 11 guessed subdomains (admin/mail/staging/test/dev-api/status/shop/billing/webmail/crm/pbx/voip) all NXDOMAIN → NO 
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (14th frozen cycle).
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token.
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage 12:00 formally INVALID (spec-silent on membership validation); drop from priority

## RANKED HYPOTHESES 2026-09-07 12:47:46 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (8 resource types) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding (arbitrary redirect_uri preserved 302→/de_CH/login for client_id=1, implicit+PKCE accepted when portal-
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/redirect_uri finding to bugs.olivermaicher.eu now — triage 12:00 graded VALID 9.1 CRITICAL-conditional; include the 302 tr
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: NO_DELTA re-verified live this cycle — token 401 invalid_client known clients / 500 nonexistent, register 500, stateless au
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (16th frozen cycle).
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — 8 new guessed subdomains (api-gw, internal, mgmt, invoice, partner, fileshare, sip, ws) all NXDOMAIN; no dang
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage-formal INVALID (spec-silent on membership validation); removed from active set.
- LEARN: ACCEPTED OTH @ auth.peoplefone.com: stateless authorize sets `redirect_uri` cookie (httponly, secure, 1-year expiry) with attacker-controlled value even on 404 
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: NEW — POST oauth/token with no client_secret → invalid_client JSON for clients 1/4/5 (confidential); nonexistent ids 2,3,10
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: NEW — 11 guessed subdomains (admin/mail/staging/test/dev-api/status/shop/billing/webmail/crm/pbx/voip) all NXDOMAIN → NO 
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (14th frozen cycle).
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token.
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage 12:00 formally INVALID (spec-silent on membership validation); drop from priority

## RANKED HYPOTHESES 2026-09-07 18:15:44 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (8 resource types) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding (arbitrary redirect_uri preserved 302→/de_CH/login for client_id=1, implicit+PKCE accepted when portal-
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/redirect_uri finding to bugs.olivermaicher.eu now — triage 12:00 graded VALID 9.1 CRITICAL-conditional; include the 302 tr
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: NO_DELTA re-verified live this cycle — token 401 invalid_client known clients / 500 nonexistent, register 500, stateless au
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (17th frozen cycle).
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — no dangling CNAME targets; reposcan yields no alternative surface.
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage-formal INVALID (spec-silent on membership validation); removed from active set.
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: NEW — POST oauth/token with no client_secret → invalid_client JSON for clients 1/4/5 (confidential); nonexistent ids 2,3,10
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: NEW — 19 guessed subdomains (admin/mail/staging/test/dev-api/status/shop/billing/webmail/crm/pbx/voip/api-gw/internal/mgm
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (16th frozen cycle).
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token.
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage 12:00 formally INVALID (spec-silent on membership validation); drop from priority
- LEARN: ACCEPTED OTH @ auth.peoplefone.com: stateless authorize sets `redirect_uri` cookie (httponly, secure, 1-year expiry) with attacker-controlled value even on 404 

## RANKED HYPOTHESES 2026-09-07 21:43:15 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (8 resource types) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: GET https://auth.peoplefone.com/de_CH/register (read-only, no cookies, ≤1 rps) — single highest-leverage passive check: 500-held ⇒ NO_DELTA (frozen 18); 
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/redirect_uri finding to bugs.olivermaicher.eu now — triage 12:00 graded VALID 9.1 CRITICAL-conditional; include the 302 tr
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: NO_DELTA re-verified frozen (register 500 / token 401 known-client & 500 nonexistent / stateless authorize 404 + attacker r
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (18th frozen cycle).
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — 19 guessed subdomains all NXDOMAIN, no wildcard, no dangling CNAME targets; reposcan yields no alternative su
- LEARN: ACCEPTED OTH @ inventory: `call-api.peoplefone.com/services/api-doc/` remains the sole unprobed breadth item across the 8-spec surface — flagged for closure thi
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: NEW — POST oauth/token with no client_secret → invalid_client JSON for clients 1/4/5 (confidential); nonexistent ids 2,3,10
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: NEW — 19 guessed subdomains all NXDOMAIN → NO wildcard DNS; no dangling CNAME targets (all → managed Cloudflare). Correct
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (17th frozen cycle).
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token.
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage-formal INVALID (spec-silent on membership validation); removed from active set.
- LEARN: ACCEPTED OTH @ auth.peoplefone.com: stateless authorize sets `redirect_uri` cookie (httponly, secure, 1-year expiry) with attacker-controlled value even on 404 

## RANKED HYPOTHESES 2026-09-07 23:49:15 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (8 resource types) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu — triage VALID 9.1 CRITICAL-conditional. Payload ready: arbitrary redirect_uri
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/redirect_uri finding to bugs.olivermaicher.eu now — triage 12:00 graded VALID 9.1 CRITICAL-conditional; include the 302 tr
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: register 500 re-verified this cycle (fresh, no cookies) — 19th frozen cycle; token-acquisition path still closed; consisten
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (19th frozen cycle).
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token.
- LEARN: ACCEPTED OTH @ inventory: `call-api.peoplefone.com/services/api-doc/` → 404 verified — inventory breadth gap closed (all 8-spec backends match the 401/404-gated
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — 19 guessed subdomains all NXDOMAIN, no wildcard, no dangling CNAME targets; reposcan yields no alternative su
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: NEW — POST oauth/token with no client_secret → invalid_client JSON for clients 1/4/5 (confidential); nonexistent ids 2,3,10
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: NEW — 19 guessed subdomains all NXDOMAIN → NO wildcard DNS; no dangling CNAME targets (all → managed Cloudflare). Correct
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (18th frozen cycle).
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token.
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage-formal INVALID (spec-silent on membership validation); removed from active set.
- LEARN: ACCEPTED OTH @ auth.peoplefone.com: stateless authorize sets `redirect_uri` cookie (httponly, secure, 1-year expiry) with attacker-controlled value even on 404 

## RANKED HYPOTHESES 2026-09-08 03:46:49 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (8 resource types) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu now — triage VALID 9.1 CRITICAL-conditional. Payload ready: arbitrary redirect
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/redirect_uri finding to bugs.olivermaicher.eu now — triage 12:00 graded VALID 9.1 CRITICAL-conditional; include the 302 tr
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: register 500 re-verified this cycle (fresh, no cookies) — 20th frozen cycle; token-acquisition path still closed; consisten
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (20th frozen cycle).
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — 19 guessed subdomains all NXDOMAIN, no wildcard, no dangling CNAME targets; reposcan yields no alternative su
- LEARN: ACCEPTED OTH @ inventory: call-api.peoplefone.com/services/api-doc/ 404 re-confirmed — inventory breadth gap remains closed (all 8-spec backends match the 401/4
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: NEW — 19 guessed subdomains all NXDOMAIN → NO wildcard DNS; no dangling CNAME targets (all → managed Cloudflare). Correct
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: NEW — POST oauth/token with no client_secret → invalid_client JSON for clients 1/4/5 (confidential); nonexistent ids 2,3,10
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (18th frozen cycle).
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token.
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage-formal INVALID (spec-silent on membership validation); removed from active set.
- LEARN: ACCEPTED OTH @ auth.peoplefone.com: stateless authorize sets `redirect_uri` cookie (httponly, secure, 1-year expiry) with attacker-controlled value even on 404 

## RANKED HYPOTHESES 2026-09-08 09:03:31 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (8 resource types) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu now — 00:30 triage VALID 7.4 (9.1 conditional). Payload ready: arbitrary redir
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: register 500 / token 401 known-clients & 500 nonexistent / stateless authorize 404+attacker redirect_uri cookie / api-doc 2
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (21st frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (21st frozen cycle); triage HOLD.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — 19 guessed subdomains all NXDOMAIN, no wildcard, no dangling CNAME targets; reposcan yields no alternative su
- LEARN: ACCEPTED OTH @ inventory: call-api.peoplefone.com/services/api-doc/ 404 reconfirmed (2026-09-07);

## RANKED HYPOTHESES 2026-09-08 13:29:58 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (8 resource types) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu now — 00:30 triage VALID 7.4 (9.1 conditional). Payload ready: arbitrary redir
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/redirect_uri finding to bugs.olivermaicher.eu now — 00:30 triage VALID 7.4 (9.1 conditional). Payload ready: arbitrary red
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: register 500 / token 401 known-clients & 500 nonexistent / stateless authorize 404+attacker redirect_uri cookie (freshly re
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (22nd frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (22nd frozen cycle); triage HOLD.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — 19 guessed subdomains all NXDOMAIN, no wildcard, no dangling CNAME targets; reposcan yields no alternative su
- LEARN: ACCEPTED OTH @ inventory: call-api.peoplefone.com/services/api-doc/ 404 reconfirmed (2026-09-07); config-api docs 404 reconfirmed this cycle.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: NEW — 19 guessed subdomains all NXDOMAIN → NO wildcard DNS; no dangling CNAME targets (all → managed Cloudflare). Correct
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: NEW — POST oauth/token with no client_secret → invalid_client JSON for clients 1/4/5 (confidential); nonexistent ids 2,3,10
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (21st frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (21st frozen cycle); triage HOLD.
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage-formal INVALID (spec-silent on membership validation); removed from active set.
- LEARN: ACCEPTED OTH @ auth.peoplefone.com: stateless authorize sets `redirect_uri` cookie (httponly, secure, 1-year expiry) with attacker-controlled value even on 404 
- LEARN: ACCEPTED OTH @ inventory: call-api.peoplefone.com/services/api-doc/ 404 reconfirmed (2026-09-07); inventory breadth gap remains closed (all 8-spec backends matc

## RANKED HYPOTHESES 2026-09-08 17:47:45 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (8 resource types) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu now — 00:30 triage VALID 7.4 (9.1 conditional). Payload ready: arbitrary redir
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu now — 00:30 triage VALID 7.4 (9.1 conditional). Payload ready: arbitrary redir
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: register 500 / token 401 known-clients & 500 nonexistent / stateless authorize 404+attacker redirect_uri cookie / api-doc 2
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (23rd frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (23rd frozen cycle); triage HOLD.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — 19 guessed subdomains all NXDOMAIN, no wildcard, no dangling CNAME targets; reposcan yields no alternative su
- LEARN: ACCEPTED OTH @ inventory: call-api.peoplefone.com/services/api-doc/ 404 reconfirmed; config-api docs 404 reconfirmed; all 8-spec backends match the 401/404-gate
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: NEW — 19 guessed subdomains all NXDOMAIN → NO wildcard DNS; no dangling CNAME targets (all → managed Cloudflare). Correct
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: NEW — POST oauth/token with no client_secret → invalid_client JSON for clients 1/4/5 (confidential); nonexistent ids 2,3,10
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (22nd frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (22nd frozen cycle); triage HOLD.
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage-formal INVALID (spec-silent on membership validation); removed from active set.
- LEARN: ACCEPTED OTH @ auth.peoplefone.com: stateless authorize sets `redirect_uri` cookie (httponly, secure, 1-year expiry) with attacker-controlled value even on 404 
- LEARN: ACCEPTED OTH @ inventory: call-api.peoplefone.com/services/api-doc/ 404 reconfirmed (2026-09-07); inventory breadth gap remains closed (all 8-spec backends matc

## RANKED HYPOTHESES 2026-09-08 20:17:44 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (from art/lead_nemotron3.txt)
- [65] peoplefone/mail-validator-mx-server/src/peoplefone/mailValidatorMXServer.php: Command Injection via Unsanitized DNS Lookup Input (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu now — 00:30 triage VALID 7.4 (9.1 conditional), sole report-ready item after 2
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu now — 00:30 triage VALID 7.4 (9.1 conditional). Payload ready: arbitrary redir
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: register 500 fresh-reverified this cycle (16:16Z, no cookies) / token 401 known-clients & 500 nonexistent / stateless autho
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (24th frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (24th frozen cycle); triage HOLD.
- LEARN: REJECTED MISCONFIG/OTHER @ repo scan: reposcan 18:10Z returns no public-org scan (TARGET_ORG unconfigured); library-level leads (mail-validator-mx-server, provi
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: NEW — 19 guessed subdomains all NXDOMAIN → NO wildcard DNS; no dangling CNAME targets (all → managed Cloudflare). Correct
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: NEW — POST oauth/token with no client_secret → invalid_client JSON for clients 1/4/5 (confidential); nonexistent ids 2,3,10
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (23rd frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (23rd frozen cycle); triage HOLD.
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage-formal INVALID (spec-silent on membership validation); removed from active set.
- LEARN: ACCEPTED OTH @ auth.peoplefone.com: stateless authorize sets `redirect_uri` cookie (httponly, secure, 1-year expiry) with attacker-controlled value even on 404 
- LEARN: ACCEPTED OTH @ inventory: call-api.peoplefone.com/services/api-doc/ 404 reconfirmed (2026-09-07); inventory breadth gap remains closed (all 8-spec backends matc

## RANKED HYPOTHESES 2026-09-08 22:46:22 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (8 resource types) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu now — 00:30 triage VALID 7.4 (9.1 conditional). Payload ready: arbitrary redir
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: NEW — 19 guessed subdomains all NXDOMAIN → NO wildcard DNS; no dangling CNAME targets (all → managed Cloudflare). Correct
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: NEW — POST oauth/token with no client_secret → invalid_client JSON for clients 1/4/5 (confidential); nonexistent ids 2,3,10
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (24th frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (24th frozen cycle); triage HOLD.
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage-formal INVALID (spec-silent on membership validation); removed from active set.
- LEARN: ACCEPTED OTH @ auth.peoplefone.com: stateless authorize sets `redirect_uri` cookie (httponly, secure, 1-year expiry) with attacker-controlled value even on 404 
- LEARN: ACCEPTED OTH @ inventory: call-api.peoplefone.com/services/api-doc/ 404 reconfirmed (2026-09-07); config-api docs 404 reconfirmed; all 8-spec backends match the

## RANKED HYPOTHESES 2026-09-09 01:13:45 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (8 resource types) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu. Triage VALID 7.4 (9.1 conditional) held across 25 frozen cycles; valid-bugs c
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu now — 00:30 triage VALID 7.4 (9.1 conditional). Payload ready: arbitrary redir
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: register 500 / token GET 405 + POST(client_id=1)→401 + POST(no-body)→500 / stateless authorize 404+attacker redirect_uri co
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (25th frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (25th frozen cycle); triage HOLD.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — no dangling CNAME targets; reposcan yields no in-scope surface.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: NEW — 19 guessed subdomains all NXDOMAIN → NO wildcard DNS; no dangling CNAME targets (all → managed Cloudflare). Correct
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: NEW — POST oauth/token with no client_secret → invalid_client JSON for clients 1/4/5 (confidential); nonexistent ids 2,3,10
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (24th frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (24th frozen cycle); triage HOLD.
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage-formal INVALID (spec-silent on membership validation); removed from active set.
- LEARN: ACCEPTED OTH @ auth.peoplefone.com: stateless authorize sets `redirect_uri` cookie (httponly, secure, 1-year expiry) with attacker-controlled value even on 404 
- LEARN: ACCEPTED OTH @ inventory: call-api.peoplefone.com/services/api-doc/ 404 reconfirmed (2026-09-07); config-api docs 404 reconfirmed; all 8-spec backends match the

## RANKED HYPOTHESES 2026-09-09 06:11:13 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (8 resource types) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu. Triage VALID 7.4 (9.1 conditional) held across 25 frozen cycles; valid-bugs c
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu now — 00:30 triage VALID 7.4 (9.1 conditional). Payload ready: arbitrary redir
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: register 500 / token GET 405 + POST(client_id=1)→401 + POST(no-body)→500 / stateless authorize 404+attacker redirect_uri co
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (25th frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (25th frozen cycle); triage HOLD.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — no dangling CNAME targets; reposcan yields no in-scope surface.
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: register 500 / token GET 405 + POST(client_id=1)→401 + POST(no-body)→500 / stateless authorize 404+attacker redirect_uri co
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (26th frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (26th frozen cycle); triage HOLD.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — no dangling CNAME targets; reposcan yields no in-scope surface.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: NEW — 19 guessed subdomains all NXDOMAIN → NO wildcard DNS; no dangling CNAME targets (all → managed Cloudflare). Correct
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: NEW — POST oauth/token with no client_secret → invalid_client JSON for clients 1/4/5 (confidential); nonexistent ids 2,3,10
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (25th frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (25th frozen cycle); triage HOLD.
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage-formal INVALID (spec-silent on membership validation); removed from active set.
- LEARN: ACCEPTED OTH @ auth.peoplefone.com: stateless authorize sets `redirect_uri` cookie (httponly, secure, 1-year expiry) with attacker-controlled value even on 404 
- LEARN: ACCEPTED OTH @ inventory: call-api.peoplefone.com/services/api-doc/ 404 reconfirmed (2026-09-07); config-api docs 404 reconfirmed; all 8-spec backends match the

## RANKED HYPOTHESES 2026-09-09 11:42:22 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (8 resource types) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu. 27th frozen cycle; valid-bugs count still 0. Exact payload verified this cycl
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu now — 00:30 triage VALID 7.4 (9.1 conditional) held across 26 frozen cycles. P
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: register 500 / token GET 405 + POST(client_id=1)→401 + POST(no-body)→500 / stateless authorize 404+attacker redirect_uri co
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (27th frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (27th frozen cycle); triage HOLD.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — no dangling CNAME targets; reposcan yields no in-scope surface.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: NEW — 19 guessed subdomains all NXDOMAIN → NO wildcard DNS; no dangling CNAME targets (all → managed Cloudflare). Correct
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: NEW — POST oauth/token with no client_secret → invalid_client JSON for clients 1/4/5 (confidential); nonexistent ids 2,3,10
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (26th frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (26th frozen cycle); triage HOLD.
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage-formal INVALID (spec-silent on membership validation); removed from active set.
- LEARN: ACCEPTED OTH @ auth.peoplefone.com: stateless authorize sets `redirect_uri` cookie (httponly, secure, 1-year expiry) with attacker-controlled value even on 404 
- LEARN: ACCEPTED OTH @ inventory: call-api.peoplefone.com/services/api-doc/ 404 reconfirmed (2026-09-07); config-api docs 404 reconfirmed; all 8-spec backends match the

## RANKED HYPOTHESES 2026-09-09 15:26:46 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (8 resource types) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu. 28th frozen cycle; valid-bugs count still 0. Exact payload verified this cycl
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu now — 00:30 triage VALID 7.4 (9.1 conditional) held across 27 frozen cycles. P
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: register 500 / token GET 405 + POST(client_id=1)→401 + POST(no-body)→500 / stateless authorize 404+attacker redirect_uri co
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (28th frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (28th frozen cycle); triage HOLD.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — no dangling CNAME targets; reposcan yields no in-scope surface.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: NEW — 19 guessed subdomains all NXDOMAIN → NO wildcard DNS; no dangling CNAME targets (all → managed Cloudflare). Correct
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: NEW — POST oauth/token with no client_secret → invalid_client JSON for clients 1/4/5 (confidential); nonexistent ids 2,3,10
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (27th frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (27th frozen cycle); triage HOLD.
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage-formal INVALID (spec-silent on membership validation); removed from active set.
- LEARN: ACCEPTED OTH @ auth.peoplefone.com: stateless authorize sets `redirect_uri` cookie (httponly, secure, 1-year expiry) with attacker-controlled value even on 404 
- LEARN: ACCEPTED OTH @ inventory: call-api.peoplefone.com/services/api-doc/ 404 reconfirmed (2026-09-07); config-api docs 404 reconfirmed; all 8-spec backends match the

## RANKED HYPOTHESES 2026-09-09 18:45:52 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (8 resource types) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu. 28th frozen cycle; valid-bugs count still 0. Exact payload verified this cycl
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu now — 00:30 triage VALID 7.4 (9.1 conditional) held across 28 frozen cycles. P
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: register 500 / token GET 405 + POST(client_id=1)→401 + POST(no-body)→500 / stateless authorize 404+attacker redirect_uri co
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (29th frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (29th frozen cycle); triage HOLD.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — no dangling CNAME targets; reposcan yields no in-scope surface.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: NEW — 19 guessed subdomains all NXDOMAIN → NO wildcard DNS; no dangling CNAME targets (all → managed Cloudflare). Correct
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: NEW — POST oauth/token with no client_secret → invalid_client JSON for clients 1/4/5 (confidential); nonexistent ids 2,3,10
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (28th frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (28th frozen cycle); triage HOLD.
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage-formal INVALID (spec-silent on membership validation); removed from active set.
- LEARN: ACCEPTED OTH @ auth.peoplefone.com: stateless authorize sets `redirect_uri` cookie (httponly, secure, 1-year expiry) with attacker-controlled value even on 404 
- LEARN: ACCEPTED OTH @ inventory: call-api.peoplefone.com/services/api-doc/ 404 reconfirmed (2026-09-07); config-api docs 404 reconfirmed; all 8-spec backends match the

## RANKED HYPOTHESES 2026-09-09 21:36:45 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (8 resource types) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu — 29th frozen cycle, valid-bugs 0. Payload re-verified fresh this cycle: `GET 
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu now — 00:30 triage VALID 7.4 (9.1 conditional) held across 29 frozen cycles. P
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: register 500 / token GET 405 + POST(client_id=1)→401 + POST(no-body)→500 / stateless authorize 404+attacker redirect_uri co
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (30th frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (30th frozen cycle); triage HOLD.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — no dangling CNAME targets; reposcan yields no in-scope surface.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: NEW — 19 guessed subdomains all NXDOMAIN → NO wildcard DNS; no dangling CNAME targets (all → managed Cloudflare). Correct
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: NEW — POST oauth/token with no client_secret → invalid_client JSON for clients 1/4/5 (confidential); nonexistent ids 2,3,10
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (29th frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (29th frozen cycle); triage HOLD.
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage-formal INVALID (spec-silent on membership validation); removed from active set.
- LEARN: ACCEPTED OTH @ auth.peoplefone.com: stateless authorize sets `redirect_uri` cookie (httponly, secure, 1-year expiry) with attacker-controlled value even on 404 
- LEARN: ACCEPTED OTH @ inventory: call-api.peoplefone.com/services/api-doc/ 404 reconfirmed (2026-09-07); config-api docs 404 reconfirmed; all 8-spec backends match the

## RANKED HYPOTHESES 2026-09-09 23:33:21 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (8 resource types) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu — 31st frozen cycle, valid-bugs 0. Payload re-verified fresh this cycle (heade
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: register 500 / token GET 405 + POST(client_id=1)→401 + POST(no-body)→500 / stateless authorize 404+attacker redirect_uri co
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (31st frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (31st frozen cycle); triage HOLD.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — no dangling CNAME targets; reposcan 23:29 ran with TARGET_ORG unconfigured, yields no in-scope surface.

## RANKED HYPOTHESES 2026-09-10 01:31:29 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (8 resource types) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu — 32nd frozen cycle, valid-bugs 0. Payload re-verified fresh this cycle: `GET 
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu now — 00:30 triage VALID 7.4 (9.1 conditional) held across 31 frozen cycles. P
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: register 500 / token GET 405 + POST(client_id=1)→401 + POST(no-body)→500 / stateless authorize 404+attacker redirect_uri co
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (32nd frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (32nd frozen cycle); triage HOLD.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — no dangling CNAME targets; reposcan yields no in-scope surface.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: NEW — 19 guessed subdomains all NXDOMAIN → NO wildcard DNS; no dangling CNAME targets (all → managed Cloudflare). Correct
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: NEW — POST oauth/token with no client_secret → invalid_client JSON for clients 1/4/5 (confidential); nonexistent ids 2,3,10
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (31st frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (31st frozen cycle); triage HOLD.
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage-formal INVALID (spec-silent on membership validation); removed from active set.
- LEARN: ACCEPTED OTH @ auth.peoplefone.com: stateless authorize sets `redirect_uri` cookie (httponly, secure, 1-year expiry) with attacker-controlled value even on 404 
- LEARN: ACCEPTED OTH @ inventory: call-api.peoplefone.com/services/api-doc/ 404 reconfirmed (2026-09-07); config-api docs 404 reconfirmed; all 8-spec backends match the

## RANKED HYPOTHESES 2026-09-10 06:43:45 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (8 resource types) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu — 32nd frozen cycle, valid-bugs 0. Payload re-verified fresh this cycle: `GET 
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu now — 00:30 triage VALID 7.4 (9.1 conditional) held across 32 frozen cycles. P
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: register 500 / token GET 405 + POST(client_id=1)→401 + POST(no-body)→500 / stateless authorize 404+attacker redirect_uri co
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (32nd frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (32nd frozen cycle); triage HOLD.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — no dangling CNAME targets; reposcan yields no in-scope surface.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: NEW — 19 guessed subdomains all NXDOMAIN → NO wildcard DNS; no dangling CNAME targets (all → managed Cloudflare). Correct
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: NEW — POST oauth/token with no client_secret → invalid_client JSON for clients 1/4/5 (confidential); nonexistent ids 2,3,10
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (32nd frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (32nd frozen cycle); triage HOLD.
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage-formal INVALID (spec-silent on membership validation); removed from active set.
- LEARN: ACCEPTED OTH @ auth.peoplefone.com: stateless authorize sets `redirect_uri` cookie (httponly, secure, 1-year expiry) with attacker-controlled value even on 404 
- LEARN: ACCEPTED OTH @ inventory: call-api.peoplefone.com/services/api-doc/ 404 reconfirmed (2026-09-07); config-api docs 404 reconfirmed; all 8-spec backends match the

## RANKED HYPOTHESES 2026-09-10 11:53:56 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (8 resource types) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu — 33rd frozen cycle, valid-bugs 0. Payload: `GET /oauth/authorize?client_id=1&
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu now — 00:30 triage VALID 7.4 (9.1 conditional) held across 32 frozen cycles. P
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: register 500 / token GET 405 + POST(client_id=1)→401 + POST(no-body)→500 / stateless authorize 404+attacker redirect_uri co
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (33rd frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (33rd frozen cycle); triage HOLD.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — no dangling CNAME targets; reposcan yields no in-scope surface.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: NEW — 19 guessed subdomains all NXDOMAIN → NO wildcard DNS; no dangling CNAME targets (all → managed Cloudflare). Correct
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: NEW — POST oauth/token with no client_secret → invalid_client JSON for clients 1/4/5 (confidential); nonexistent ids 2,3,10
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (32nd frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (32nd frozen cycle); triage HOLD.
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage-formal INVALID (spec-silent on membership validation); removed from active set.
- LEARN: ACCEPTED OTH @ auth.peoplefone.com: stateless authorize sets `redirect_uri` cookie (httponly, secure, 1-year expiry) with attacker-controlled value even on 404 
- LEARN: ACCEPTED OTH @ inventory: call-api.peoplefone.com/services/api-doc/ 404 reconfirmed (2026-09-07); config-api docs 404 reconfirmed; all 8-spec backends match the

## RANKED HYPOTHESES 2026-09-10 16:08:02 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (8 resource types) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu — 34th frozen cycle, valid-bugs 0. Payload: `GET /oauth/authorize?client_id=1&
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu now — 33rd frozen cycle, triage VALID 7.4 (9.1 conditional). Payload: `GET /oa
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: register 500 / token GET 405 + POST(client_id=1)→401 + POST(no-body)→500 / stateless authorize 404+attacker redirect_uri co
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (34th frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (34th frozen cycle); triage HOLD.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — no dangling CNAME targets; reposcan yields no in-scope surface.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: NEW — 19 guessed subdomains all NXDOMAIN → NO wildcard DNS; no dangling CNAME targets (all → managed Cloudflare). Correct
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: NEW — POST oauth/token with no client_secret → invalid_client JSON for clients 1/4/5 (confidential); nonexistent ids 2,3,10
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (33rd frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (33rd frozen cycle); triage HOLD.
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage-formal INVALID (spec-silent on membership validation); removed from active set.
- LEARN: ACCEPTED OTH @ auth.peoplefone.com: stateless authorize sets `redirect_uri` cookie (httponly, secure, 1-year expiry) with attacker-controlled value even on 404 
- LEARN: ACCEPTED OTH @ inventory: call-api.peoplefone.com/services/api-doc/ 404 reconfirmed (2026-09-07); config-api docs 404 reconfirmed; all 8-spec backends match the

## RANKED HYPOTHESES 2026-09-10 19:16:12 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (8 resource types) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu — 34th frozen cycle, valid-bugs 0. Payload: `GET /oauth/authorize?client_id=1&
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu now — 33rd frozen cycle, triage VALID 7.4 (9.1 conditional). Payload: `GET /oa
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: register 500 / token GET 405 + POST(client_id=1)→401 + POST(no-body)→500 / stateless authorize 404+attacker redirect_uri co
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (34th frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (34th frozen cycle); triage HOLD.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — no dangling CNAME targets; reposcan yields no in-scope surface.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: NEW — 19 guessed subdomains all NXDOMAIN → NO wildcard DNS; no dangling CNAME targets (all → managed Cloudflare). Correct
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: NEW — POST oauth/token with no client_secret → invalid_client JSON for clients 1/4/5 (confidential); nonexistent ids 2,3,10
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (33rd frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (33rd frozen cycle); triage HOLD.
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage-formal INVALID (spec-silent on membership validation); removed from active set.
- LEARN: ACCEPTED OTH @ auth.peoplefone.com: stateless authorize sets `redirect_uri` cookie (httponly, secure, 1-year expiry) with attacker-controlled value even on 404 
- LEARN: ACCEPTED OTH @ inventory: call-api.peoplefone.com/services/api-doc/ 404 reconfirmed (2026-09-07); config-api docs 404 reconfirmed; all 8-spec backends match the

## RANKED HYPOTHESES 2026-09-10 21:45:47 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (8 resource types) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu — 35th frozen cycle, valid-bugs 0. Payload: `GET /oauth/authorize?client_id=1&
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu now — 34th frozen cycle, triage VALID 7.4 (9.1 conditional). Payload: `GET /oa
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: register 500 / token GET 405 + POST(client_id=1)→401 + POST(no-body)→500 / stateless authorize 404+attacker redirect_uri co
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (35th frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (35th frozen cycle); triage HOLD.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — no dangling CNAME targets; reposcan yields no in-scope surface.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: NEW — 19 guessed subdomains all NXDOMAIN → NO wildcard DNS; no dangling CNAME targets (all → managed Cloudflare). Correct
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: NEW — POST oauth/token with no client_secret → invalid_client JSON for clients 1/4/5 (confidential); nonexistent ids 2,3,10
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (34th frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (34th frozen cycle); triage HOLD.
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage-formal INVALID (spec-silent on membership validation); removed from active set.
- LEARN: ACCEPTED OTH @ auth.peoplefone.com: stateless authorize sets `redirect_uri` cookie (httponly, secure, 1-year expiry) with attacker-controlled value even on 404 
- LEARN: ACCEPTED OTH @ inventory: call-api.peoplefone.com/services/api-doc/ 404 reconfirmed (2026-09-07); config-api docs 404 reconfirmed; all 8-spec backends match the

## RANKED HYPOTHESES 2026-09-10 23:53:32 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (8 resource types) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: stateless GET (≤1 rps) alternate registration routes on auth.peoplefone.com: `/register`, `/en_CH/register`, `/fr_CH/register`, `/it_CH/register`, `/de_D
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu now — 35th frozen cycle, triage VALID 7.4 (9.1 conditional). Payload: `GET /oa
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: NEW — 19 guessed subdomains all NXDOMAIN → NO wildcard DNS; no dangling CNAME targets (all → managed Cloudflare). Correct
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: NEW — POST oauth/token with no client_secret → invalid_client JSON for clients 1/4/5 (confidential); nonexistent ids 2,3,10
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (35th frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (35th frozen cycle); triage HOLD.
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage-formal INVALID (spec-silent on membership validation); removed from active set.
- LEARN: ACCEPTED OTH @ auth.peoplefone.com: stateless authorize sets `redirect_uri` cookie (httponly, secure, 1-year expiry) with attacker-controlled value even on 404 
- LEARN: ACCEPTED OTH @ inventory: call-api.peoplefone.com/services/api-doc/ 404 reconfirmed (2026-09-07); config-api docs 404 reconfirmed; all 8-spec backends match the

## RANKED HYPOTHESES 2026-09-11 03:48:31 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (8 resource types) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu — 36th frozen cycle, valid-bugs 0, register-minting lever now proven permanent
- NEXT(hypotheses-nemotron3.txt): PROBE: stateless GET (≤1 rps) alternate registration routes on auth.peoplefone.com: `/register`, `/en_CH/register`, `/fr_CH/register`, `/it_CH/register`, `/de_D
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: all locale variants of /register (en_CH/fr_CH/it_CH/de_DE/en_GB) → 500, bare /register → 404 — register-500 regression is G
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: register 500 / token GET 405 + POST(client_id=1)→401 + POST(no-body)→500 / stateless authorize 404+attacker redirect_uri co
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (36th frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (36th frozen cycle); triage HOLD.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — 19 guessed subdomains all NXDOMAIN, no wildcard, no dangling CNAME targets; reposcan yields no in-scope surfa
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: 19 guessed subdomains all NXDOMAIN → NO wildcard DNS; no dangling CNAME targets (all → managed Cloudflare). Corrects file
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: POST /oauth/token no client_secret → invalid_client JSON for clients 1/4/5 (confidential); nonexistent ids 2,3,10,100,999,0
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (35th frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (35th frozen cycle); triage HOLD.
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage-formal INVALID (spec-silent on membership validation); removed from active set.
- LEARN: ACCEPTED OTH @ auth.peoplefone.com: stateless authorize sets `redirect_uri` cookie (httponly, secure, 1-year expiry) with attacker-controlled value even on 404 
- LEARN: ACCEPTED OTH @ inventory: call-api.peoplefone.com/services/api-doc/ 404 reconfirmed (2026-09-07); config-api docs 404 reconfirmed; all 8-spec backends match the

## RANKED HYPOTHESES 2026-09-11 08:47:53 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (from art/lead_nemotron3.txt)
- [62] auth.peoplefone.com/oauth/authorize: OAuth open-redirect + login-CSRF on auth (client_id=1), cookie-seeded variant (from art/lead_bigpickle.txt)
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu now — 36th frozen cycle, triage VALID 7.4 (9.1 conditional). Payload: `GET /oa
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: all locale variants of /register (en_CH/fr_CH/it_CH/de_DE/en_GB) → 500, bare /register → 404 — register-500 regression is G
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: register 500 / token GET 405 + POST(client_id=1)→401 + POST(no-body)→500 / stateless authorize 404+attacker redirect_uri co
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (36th frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (36th frozen cycle); triage HOLD.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — 19 guessed subdomains all NXDOMAIN, no wildcard, no dangling CNAME targets; reposcan yields no in-scope surfa
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage-formal INVALID (spec-silent on membership validation); removed from active set.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: 19 guessed subdomains all NXDOMAIN → NO wildcard DNS; no dangling CNAME targets (all → managed Cloudflare). Corrects file
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: POST /oauth/token no client_secret → invalid_client JSON for clients 1/4/5 (confidential); nonexistent ids 2,3,10,100,999,0
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (36th frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (36th frozen cycle); triage HOLD.
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage-formal INVALID (spec-silent on membership validation); removed from active set.
- LEARN: ACCEPTED OTH @ auth.peoplefone.com: stateless authorize sets `redirect_uri` cookie (httponly, secure, 1-year expiry) with attacker-controlled value even on 404 
- LEARN: ACCEPTED OTH @ inventory: call-api.peoplefone.com/services/api-doc/ 404 reconfirmed (2026-09-07); config-api docs 404 reconfirmed; all 8-spec backends match the

## RANKED HYPOTHESES 2026-09-11 13:25:34 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (from art/lead_nemotron3.txt)
- [62] auth.peoplefone.com/oauth/authorize: OAuth open-redirect + login-CSRF on auth (client_id=1), cookie-seeded variant (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu — 36th frozen cycle, valid-bugs 0, and this cycle's breadth sweep (Laravel deb
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu now — 36th frozen cycle, triage VALID 7.4 (9.1 conditional). Payload: `GET /oa
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: 19 guessed subdomains all NXDOMAIN → NO wildcard DNS; no dangling CNAME targets (all → managed Cloudflare). Corrects file
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: POST /oauth/token no client_secret → invalid_client JSON for clients 1/4/5 (confidential); nonexistent ids 2,3,10,100,999,0
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (36th frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (36th frozen cycle); triage HOLD.
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage-formal INVALID (spec-silent on membership validation); removed from active set.
- LEARN: ACCEPTED OTH @ auth.peoplefone.com: stateless authorize sets `redirect_uri` cookie (httponly, secure, 1-year expiry) with attacker-controlled value even on 404 
- LEARN: ACCEPTED OTH @ inventory: call-api.peoplefone.com/services/api-doc/ 404 reconfirmed (2026-09-07); config-api docs 404 reconfirmed; all 8-spec backends match the

## RANKED HYPOTHESES 2026-09-11 17:16:44 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (8 resource types) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu — 37th frozen cycle, valid-bugs 0, and this cycle's breadth sweep (Laravel deb
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu now — 36th frozen cycle, triage VALID 7.4 (9.1 conditional). Payload: `GET /oa
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: register 500 / token GET 405 + POST(client_id=1)→401 + POST(no-body)→500 / stateless authorize 404+attacker redirect_uri co
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (37th frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (37th frozen cycle); triage HOLD.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — 19 guessed subdomains all NXDOMAIN, no wildcard, no dangling CNAME targets; reposcan yields no in-scope surfa
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage-formal INVALID (spec-silent on membership validation); removed from active set.
- LEARN: ACCEPTED OTH @ auth.peoplefone.com: stateless authorize sets `redirect_uri` cookie (httponly, secure, 1-year expiry) with attacker-controlled value even on 404 
- LEARN: ACCEPTED OTH @ inventory: call-api.peoplefone.com/services/api-doc/ 404 reconfirmed; config-api docs 404 reconfirmed; all 8-spec backends match the 401/404-gate
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: 19 guessed subdomains all NXDOMAIN → NO wildcard DNS; no dangling CNAME targets (all → managed Cloudflare). Corrects file
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: POST /oauth/token no client_secret → invalid_client JSON for clients 1/4/5 (confidential); nonexistent ids 2,3,10,100,999,0
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (36th frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (36th frozen cycle); triage HOLD.
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage-formal INVALID (spec-silent on membership validation); removed from active set.
- LEARN: ACCEPTED OTH @ auth.peoplefone.com: stateless authorize sets `redirect_uri` cookie (httponly, secure, 1-year expiry) with attacker-controlled value even on 404 
- LEARN: ACCEPTED OTH @ inventory: call-api.peoplefone.com/services/api-doc/ 404 reconfirmed (2026-09-07); config-api docs 404 reconfirmed; all 8-spec backends match the

## RANKED HYPOTHESES 2026-09-11 19:51:32 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (8 resource types) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu — 37th frozen cycle, valid-bugs 0, and this cycle's breadth sweep (Laravel deb
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu now — 37th frozen cycle, triage VALID 7.4 (9.1 conditional). Payload: `GET /oa
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: register 500 / token GET 405 + POST(client_id=1)→401 + POST(no-body)→500 / stateless authorize 404+attacker redirect_uri co
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (37th frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (37th frozen cycle); triage HOLD.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — 19 guessed subdomains all NXDOMAIN, no wildcard, no dangling CNAME targets; reposcan yields no in-scope surfa
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage-formal INVALID (spec-silent on membership validation); removed from active set.
- LEARN: ACCEPTED OTH @ auth.peoplefone.com: stateless authorize sets `redirect_uri` cookie (httponly, secure, 1-year expiry) with attacker-controlled value even on 404 
- LEARN: ACCEPTED OTH @ inventory: call-api.peoplefone.com/services/api-doc/ 404 reconfirmed; config-api docs 404 reconfirmed; all 8-spec backends match the 401/404-gate
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: register 500 / token 405 / stateless authorize 404+attacker redirect_uri cookie (Max-Age 34560000, header-level fresh re-ve
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (38th frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (38th frozen cycle); triage HOLD.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — 19 guessed subdomains all NXDOMAIN, no wildcard, no dangling CNAME targets; reposcan yields no in-scope surfa
- LEARN: ACCEPTED OTH @ inventory: status map identical — api docs 200, config-api docs 404, call-api docs 404; all 8-spec backends match the 401/404-gated real-backend 
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: 19 guessed subdomains all NXDOMAIN → NO wildcard DNS; no dangling CNAME targets (all → managed Cloudflare). Corrects file
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: POST /oauth/token no client_secret → invalid_client JSON for clients 1/4/5 (confidential); nonexistent ids 2,3,10,100,999,0
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (37th frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (37th frozen cycle); triage HOLD.
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage-formal INVALID (spec-silent on membership validation); removed from active set.
- LEARN: ACCEPTED OTH @ auth.peoplefone.com: stateless authorize sets `redirect_uri` cookie (httponly, secure, 1-year expiry) with attacker-controlled value even on 404 
- LEARN: ACCEPTED OTH @ inventory: call-api.peoplefone.com/services/api-doc/ 404 reconfirmed (2026-09-07); config-api docs 404 reconfirmed; all 8-spec backends match the

## RANKED HYPOTHESES 2026-09-11 22:23:05 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (from art/lead_nemotron3.txt)
- [62] auth.peoplefone.com/oauth/authorize: OAuth open-redirect + login-CSRF on auth (client_id=1), cookie-seeded variant (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu — 38th frozen cycle, valid-bugs 0. Payload `GET /oauth/authorize?client_id=1&r
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu now — 38th frozen cycle, triage VALID 7.4 (9.1 conditional). Payload: `GET /oa
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: register 500 / token 405 / stateless authorize 404+attacker redirect_uri cookie (Max-Age 34560000, header-level fresh re-ve
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (38th frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (38th frozen cycle); triage HOLD.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — 19 guessed subdomains all NXDOMAIN, no wildcard, no dangling CNAME targets; reposcan yields no in-scope surfa
- LEARN: ACCEPTED OTH @ inventory: status map identical — api docs 200, config-api docs 404, call-api docs 404; all 8-spec backends match the 401/404-gated real-backend 
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: register 500 / token 405 / stateless authorize 404+attacker redirect_uri cookie / api-doc 200 / config+call docs 404 — NO_D
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (39th frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (39th frozen cycle); triage HOLD.
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — 19 guessed subdomains all NXDOMAIN, no wildcard, no dangling CNAME targets; reposcan (TARGET_ORG unconfigured
- LEARN: ACCEPTED OTH @ pipeline: triage runs 2026-09-11 18:58Z and 21:36Z (mimo-v2.5-free) received EMPTY leads ("No leads were provided") — the triage channel is not r
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: 19 guessed subdomains all NXDOMAIN → NO wildcard DNS; no dangling CNAME targets (all → managed Cloudflare). Corrects file
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: POST /oauth/token no client_secret → invalid_client JSON for clients 1/4/5 (confidential); nonexistent ids 2,3,10,100,999,0
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (38th frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (38th frozen cycle); triage HOLD.
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage-formal INVALID (spec-silent on membership validation); removed from active set.
- LEARN: ACCEPTED OTH @ auth.peoplefone.com: stateless authorize sets `redirect_uri` cookie (httponly, secure, 1-year expiry) with attacker-controlled value even on 404 
- LEARN: ACCEPTED OTH @ inventory: call-api.peoplefone.com/services/api-doc/ 404 reconfirmed (2026-09-07); config-api docs 404 reconfirmed; all 8-spec backends match the

## RANKED HYPOTHESES 2026-09-12 00:26:36 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (8 resource types) (from art/lead_bigpickle.txt)
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu now — 39th frozen cycle, triage VALID 7.4 (9.1 conditional). Payload: `GET /oa
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: 19 guessed subdomains all NXDOMAIN → NO wildcard DNS; no dangling CNAME targets (all → managed Cloudflare). Corrects file
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: POST /oauth/token no client_secret → invalid_client JSON for clients 1/4/5 (confidential); nonexistent ids 2,3,10,100,999,0
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (39th frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (39th frozen cycle); triage HOLD.
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage-formal INVALID (spec-silent on membership validation); removed from active set.
- LEARN: ACCEPTED OTH @ auth.peoplefone.com: stateless authorize sets `redirect_uri` cookie (httponly, secure, 1-year expiry) with attacker-controlled value even on 404 
- LEARN: ACCEPTED OTH @ inventory: call-api.peoplefone.com/services/api-doc/ 404 reconfirmed (2026-09-07); config-api docs 404 reconfirmed; all 8-spec backends match the

## RANKED HYPOTHESES 2026-09-12 05:03:55 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (from art/lead_nemotron3.txt)
- [62] auth.peoplefone.com/oauth/authorize: OAuth open-redirect + login-CSRF on auth (client_id=1), cookie-seeded variant (from art/lead_bigpickle.txt)
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu now — 39th frozen cycle, triage VALID 7.4 (9.1 conditional). Payload: `GET /oa
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: 19 guessed subdomains all NXDOMAIN → NO wildcard DNS; no dangling CNAME targets (all → managed Cloudflare). Corrects file
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: POST /oauth/token no client_secret → invalid_client JSON for clients 1/4/5 (confidential); nonexistent ids 2,3,10,100,999,0
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (39th frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (39th frozen cycle); triage HOLD.
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage-formal INVALID (spec-silent on membership validation); removed from active set.
- LEARN: ACCEPTED OTH @ auth.peoplefone.com: stateless authorize sets `redirect_uri` cookie (httponly, secure, 1-year expiry) with attacker-controlled value even on 404 
- LEARN: ACCEPTED OTH @ inventory: call-api.peoplefone.com/services/api-doc/ 404 reconfirmed (2026-09-07); config-api docs 404 reconfirmed; all 8-spec backends match the

## RANKED HYPOTHESES 2026-09-12 09:29:02 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (from art/lead_nemotron3.txt)
- [62] auth.peoplefone.com/oauth/authorize: OAuth open-redirect + login-CSRF on auth (client_id=1), cookie-seeded variant (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding now to bugs.olivermaicher.eu — 40th frozen cycle, triage VALID 7.4 (9.1 conditional). Payload: `GET /oa
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu now — 39th frozen cycle, triage VALID 7.4 (9.1 conditional). Payload: `GET /oa
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: 19 guessed subdomains all NXDOMAIN → NO wildcard DNS; no dangling CNAME targets (all → managed Cloudflare). Corrects file
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: POST /oauth/token no client_secret → invalid_client JSON for clients 1/4/5 (confidential); nonexistent ids 2,3,10,100,999,0
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (39th frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (39th frozen cycle); triage HOLD.
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage-formal INVALID (spec-silent on membership validation); removed from active set.
- LEARN: ACCEPTED OTH @ auth.peoplefone.com: stateless authorize sets `redirect_uri` cookie (httponly, secure, 1-year expiry) with attacker-controlled value even on 404 
- LEARN: ACCEPTED OTH @ inventory: call-api.peoplefone.com/services/api-doc/ 404 reconfirmed (2026-09-07); config-api docs 404 reconfirmed; all 8-spec backends match the

## RANKED HYPOTHESES 2026-09-12 13:11:07 UTC
- [85] configuration-api.peoplefone.com/customer/voip/v1/{users,groups,ivrs,queues,numbers,smart-routings,callforwarding,manual-routing}/{identifier}: Cross-tenant PBX takeover via Configuration API sequential identifier enumeration (from art/lead_nemotron3.txt)
- [62] auth.peoplefone.com/oauth/authorize: OAuth open-redirect + login-CSRF on auth (client_id=1), cookie-seeded variant (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding now to bugs.olivermaicher.eu — 40th frozen cycle, triage VALID 7.4 (9.1 conditional). Payload: `GET /oa
- NEXT(hypotheses-nemotron3.txt): HUMAN: Submit the OAuth open-redirect/login-CSRF finding to bugs.olivermaicher.eu now — 39th frozen cycle, triage VALID 7.4 (9.1 conditional). Payload: `GET /oa
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: register 500 / token GET 405 + POST(client_id=1)→401 + POST(no-body)→500 / stateless authorize 404+attacker redirect_uri co
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (40th frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (40th frozen cycle); triage HOLD.
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage-formal INVALID (spec-silent on membership validation); removed from active set.
- LEARN: ACCEPTED OTH @ auth.peoplefone.com: stateless authorize sets `redirect_uri` cookie (httponly, secure, 1-year expiry) with attacker-controlled value even on 404 
- LEARN: ACCEPTED OTH @ inventory: call-api.peoplefone.com/services/api-doc/ 404 reconfirmed; config-api docs 404 reconfirmed; all 8-spec backends match the 401/404-gate
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: unchanged — 19 guessed subdomains all NXDOMAIN, no wildcard, no dangling CNAME targets; reposcan yields no in-scope surfa
- LEARN: REJECTED MISCONFIG @ *.peoplefone.com: 19 guessed subdomains all NXDOMAIN → NO wildcard DNS; no dangling CNAME targets (all → managed Cloudflare). Corrects file
- LEARN: ACCEPTED AUTH @ auth.peoplefone.com: POST /oauth/token no client_secret → invalid_client JSON for clients 1/4/5 (confidential); nonexistent ids 2,3,10,100,999,0
- LEARN: ACCEPTED IDOR @ configuration-api {identifier} CRUD: no counter-evidence; rank holds; token-gated (39th frozen cycle); triage HOLD pending bearer token.
- LEARN: ACCEPTED SSRF @ 5 callback endpoints: no counter-evidence; retained pending token (39th frozen cycle); triage HOLD.
- LEARN: REJECTED BUSLOGIC @ call-api queue agents: triage-formal INVALID (spec-silent on membership validation); removed from active set.
- LEARN: ACCEPTED OTH @ auth.peoplefone.com: stateless authorize sets `redirect_uri` cookie (httponly, secure, 1-year expiry) with attacker-controlled value even on 404 
- LEARN: ACCEPTED OTH @ inventory: call-api.peoplefone.com/services/api-doc/ 404 reconfirmed (2026-09-07); config-api docs 404 reconfirmed; all 8-spec backends match the
