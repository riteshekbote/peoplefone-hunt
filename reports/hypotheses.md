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
