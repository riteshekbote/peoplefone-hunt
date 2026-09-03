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
