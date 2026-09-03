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

## DEEP SERVICE SCAN 2026-09-02 (read-only connect+banner)
**Host:** `api.peoplefone.com` | **Ports:** [80, 443, 2082, 2083, 2086, 2087, 8080, 8443]
**Non-web ports observed:** [2082, 2083, 2086, 2087, 8080, 8443]
> NOTE: repeated identical non-web port sets (e.g. 2082,2083,2086,2087,8080,8443) across many hosts and wide port sets are likely a shared edge/proxy answering EOF, NOT confirmed real services. Verify with a proper port scanner (e.g. nmap) under authorization before treating as real. These are surface-map hints only, not findings.

## DEEP SERVICE SCAN 2026-09-02 (read-only connect+banner)
**Host:** `support.peoplefone.com` | **Ports:** [80, 443, 2082, 2083, 2086, 2087, 8080, 8443]
**Non-web ports observed:** [2082, 2083, 2086, 2087, 8080, 8443]
> NOTE: repeated identical non-web port sets (e.g. 2082,2083,2086,2087,8080,8443) across many hosts and wide port sets are likely a shared edge/proxy answering EOF, NOT confirmed real services. Verify with a proper port scanner (e.g. nmap) under authorization before treating as real. These are surface-map hints only, not findings.

## 2026-09-02 21:54:06 UTC

## 2026-09-02 23:55:44 UTC

## 2026-09-03 03:38:09 UTC

## 2026-09-03 08:20:18 UTC
