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
