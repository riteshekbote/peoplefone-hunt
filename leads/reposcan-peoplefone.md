## REPOSCAN 2026-09-03 15:10:38 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-03 18:41:50 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-03 21:29:14 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-03 23:32:41 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-04 01:18:26 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-04 06:01:10 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-04 10:35:25 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-04 14:31:30 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-04 17:45:39 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-04 19:59:58 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-04 22:10:09 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-05 00:09:01 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-05 04:32:17 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-05 08:33:49 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-05 12:00:07 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-05 14:46:45 UTC
[HYP] Command Injection via Unsanitized DNS Lookup Input
class: SSRF
asset: peoplefone/mail-validator-mx-server/src/peoplefone/mailValidatorMXServer.php
confidence: 65
reasoning: getMXDomains() passes $host (derived from user-supplied email domain) directly
impact: medium
verify_steps: 1) Confirm the class is used in any Peoplefone backend service handling
[HYP] SSRF via Unvalidated MX Server Connection
class: SSRF
asset: peoplefone/mail-validator-mx-server/src/peoplefone/mailValidatorMXServer.php
confidence: 55
reasoning: getMXConnection() calls fsockopen($host, $this->sock_port, ...) where $host
impact: medium
verify_steps: 1) Register a domain with MX record pointing to 169.254.169.254.
[HYP] Hardcoded Third-Party Provisioning API Endpoints
class: OTHER
asset: peoplefone/provisioning-rpc/src/ProvisioningRPCDevice{Auerswald,Gigaset,Panasonic,Snom,Yealink}.php
confidence: 90
reasoning: Five device classes contain hardcoded base URIs for external provisioning
impact: low
verify_steps: 1) Confirm these endpoints are still live/vendor-operated.
[HYP] Test File References External Credential File
class: OTHER
asset: peoplefone/provisioning-rpc/tests/test.php
confidence: 40
reasoning: test.php includes a file at __DIR__.'/../../provisioning-rpc-settings.php'
impact: info
verify_steps: 1) Confirm provisioning-rpc-settings.php is never committed in any
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-05 17:00:03 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-05 18:49:12 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-05 20:48:09 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-05 22:27:34 UTC
class: OTHER
asset: provisioning-rpc/src/ProvisioningRPCDevice{Snom,Panasonic,Gigaset,Auerswald,Yealink}.php
confidence: 25
reasoning: Each device class hardcodes a third-party provisioning endpoint URL (e.g. `https://secure-provisioning.snom.com:8083`, `https://prov.gigaset.net`, `https://api-dm.yealink.com:8443`, `https://provisioning.auerswald.de`, `https://provisioning.e-connecting.net`) and a default constructor parameter `$client_auth=['username','password']`. The test file `provisioning-rpc/tests/test.php` also falls back to `$login = ['username', 'password']`. These are clearly **dummy placeholder values**, not live credentials. The endpoint URLs belong to third-party phone vendors, not to peoplefone infrastructure.
impact: informational (no live secret leaked; placeholder values only; third-party endpoints are public API docs)
verify_steps: Verify that no deployment artifact ships with real credentials substituted into these constructors. Check `provisioning-rpc-settings.php` (referenced in tests via `file_exists`) is `.gitignore`d and never committed — the `.gitignore` should be confirmed.
class: OTHER
asset: provisioning-rpc/src/ProvisioningRPC.php:9
confidence: 30
reasoning: `ProvisioningRPC::connect($model, $login)` builds a class name as `get_class().'Device'.ucfirst(strtolower($model))` and does `new $classname($login)`. If `$model` originates from external input, this is a class-injection vector constrained to the `Peoplefone\ProvisioningRPCDevice*` namespace. The catch block uses `die($t->getMessage())` which leaks the exception string.
impact: low (namespace-constrained; requires caller to pass unsanitized input; `die()` leaks error messages but not stack traces)
verify_steps: Check all call sites of `ProvisioningRPC::connect()` to confirm `$model` is never user-supplied. If it is, whitelist allowed model names.
class: SSRF
asset: provisioning-rpc/src/ProvisioningRPCDevice{Snom,Panasonic,Gigaset,Auerswald,Yealink}.php — `addPhone()` methods
confidence: 20
reasoning: The `$url` parameter in `addPhone(string $mac, string $url, ...)` is passed directly into the XML-RPC call body to the third-party provisioning server without any URL validation (no scheme/hostname allowlist). If a calling application passes user-controlled input as `$url`, the phone would be directed to fetch its provisioning from an attacker-chosen URL, enabling phone-level MITM or firmware redirection. The `$url` is not fetched by the peoplefone server itself; the phone fetches it.
impact: medium (only exploitable if the calling web app exposes `addPhone()` with user-controlled `$url`; impact is phone-level config hijack, not server-side)
verify_steps: Identify the web application(s) that consume this library and check whether `addPhone()` receives user-supplied URLs. If so, validate against an allowlist of known provisioning domains.
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-06 00:11:15 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-06 04:42:06 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-06 09:01:41 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-06 12:54:36 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-06 15:52:59 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
