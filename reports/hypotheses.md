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
