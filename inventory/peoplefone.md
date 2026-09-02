# peoplefone GmbH inventory (discovery seed 2026-09-02)
# NOTE: hosts below are discovery candidates from passive DNS/CT; confirm in-scope vs program scope before active testing.
api.peoplefone.com
auth.peoplefone.com
peoplefone.com
support.peoplefone.com
www.peoplefone.com

## PASSIVE RECON 2026-09-02 (read-only, non-intrusive)

> Recon observations only. These are NOT confirmed vulnerabilities; ownership/in-scope of each host must be confirmed against the program scope before any active testing. Hosts resolve + serve HTTP — investigation requires scoped authorization.

**Probed:** 5 hosts | **Live HTTP:** 2

| Host | Status | Server/Tech |
|---|---|---|
| `api.peoplefone.com` | 302 | Server: cloudflare -> https://www.peoplefone.com/en-ch/developer |
| `support.peoplefone.com` | 302 | Server: cloudflare -> https://support.peoplefone.com/che/willkommen/ |

**CNAME review signals (2):**
- `api.peoplefone.com` -> `api.peoplefone.com.cdn.cloudflare.net`
- `support.peoplefone.com` -> `support.peoplefone.com.cdn.cloudflare.net`
