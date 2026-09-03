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
