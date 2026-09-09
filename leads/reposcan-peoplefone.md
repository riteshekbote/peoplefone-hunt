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
## REPOSCAN 2026-09-06 17:53:25 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-06 19:43:03 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-06 21:50:55 UTC
[HYP] Command Injection via Unsanitized DNS Lookup Input
class: SSRF
asset: peoplefone/mail-validator-mx-server/src/peoplefone/mailValidatorMXServer.php:242-246
confidence: 70
reasoning: getMXDomains() extracts domain from user-supplied email, performs minimal regex sanitize (/[^a-z0-9\-\.]/), then passes $host directly into exec("nslookup -querytype=mx ".$host) and exec("dig mx ".$host." | grep ..."). The regex allows hyphens and dots but does NOT prevent injection of shell metacharacters beyond basic alphanumeric+dot+hyphen. However, the regex is strict enough to block most shell injection vectors. The SSRF risk is that an attacker-controlled MX domain could point to internal infrastructure (169.254.169.254, 10.x, etc.) and the server would connect to it via fsockopen on port 25.
impact: medium
verify_steps: 1) Register a domain with MX record pointing to 169.254.169.254 or internal IP. 2) Pass an email address using that domain to the validator. 3) Confirm the server attempts SMTP connection to the attacker-controlled IP.
[HYP] SSRF via Unvalidated MX Server Connection
class: SSRF
asset: peoplefone/mail-validator-mx-server/src/peoplefone/mailValidatorMXServer.php:274
confidence: 60
reasoning: getMXConnection() calls fsockopen($host, $this->sock_port, ...) where $host comes from DNS MX lookup results. No IP range validation or allowlist is performed. An attacker who controls DNS for a domain can point MX records to internal/private IPs (RFC 1918, link-local, cloud metadata endpoints). The connection is outbound SMTP on port 25.
impact: medium
verify_steps: 1) Create a domain with MX record pointing to 169.254.169.254 (AWS metadata). 2) Use mailValidatorMXServer to validate an email on that domain. 3) Observe connection attempt to the metadata endpoint.
[HYP] Hardcoded Third-Party Provisioning API Endpoints
class: OTHER
asset: peoplefone/provisioning-rpc/src/ProvisioningRPCDevice{Auerswald,Gigaset,Panasonic,Snom,Yealink}.php
confidence: 90
reasoning: Five device classes contain hardcoded base URIs for external vendor provisioning APIs: https://secure-provisioning.snom.com:8083, https://prov.gigaset.net, https://api-dm.yealink.com:8443, https://provisioning.auerswald.de, https://provisioning.e-connecting.net. These are third-party phone vendor endpoints, not peoplefone infrastructure. The constructor default parameter $client_auth=['username','password'] is a placeholder, not a real credential.
impact: low (third-party public endpoints; no live credentials leaked)
verify_steps: 1) Confirm these endpoints are still live/vendor-operated. 2) Verify provisioning-rpc-settings.php (referenced in tests) is .gitignore'd and never committed.
[HYP] Test File References External Credential File
class: OTHER
asset: peoplefone/provisioning-rpc/tests/test.php:7-9
confidence: 40
reasoning: test.php includes a file at __DIR__.'/../../provisioning-rpc-settings.php' via file_exists() check. If this settings file were ever committed, it would contain real credentials ($auerswald_login, $gigaset_login, etc.). The .gitignore does NOT explicitly exclude provisioning-rpc-settings.php (only vendor, composer.lock, .idea are listed).
impact: info (no settings file committed; but .gitignore incomplete)
verify_steps: 1) Confirm provisioning-rpc-settings.php is never committed in any branch/commit history. 2) Add provisioning-rpc-settings.php to .gitignore to prevent accidental commit.
[HYP] Default Credential Placeholder in Constructor Signatures
class: OTHER
asset: peoplefone/provisioning-rpc/src/ProvisioningRPCDevice{Snom,Panasonic,Gigaset,Auerswald,Yealink}.php
confidence: 25
reasoning: Each device class has constructor default $client_auth=['username','password']. These are clearly dummy placeholder values, not live credentials. The test file also uses ['username', 'password'] as fallback. These are not secrets but represent a code smell that could lead to accidental credential exposure if a developer copies the pattern without proper credential management.
impact: informational (no live secret; placeholder values only)
verify_steps: Verify no deployment artifact ships with real credentials substituted into these constructors.
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-06 23:19:54 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-07 01:08:45 UTC
[HYP] Command Injection via unsanitized `$host` in `exec()` call
class: SSRF
asset: peoplefone/mail-validator-mx-server/src/peoplefone/mailValidatorMXServer.php:242-245
confidence: 75
reasoning: `getMXDomains()` concatenates `$host` (derived from user-supplied email address) directly into `exec("nslookup -querytype=mx ".$host)` and `exec("dig mx ".$host." | grep -v '^;' | grep ".$host)`. The constructor regex `/[^a-z0-9\-\.]/` strips most chars but permits `.`, `-`, `@` and backtick ` ` which is a shell metacharacter. An attacker-controlled email like `foo\`id\`@evil.com` would pass the regex filter and get interpolated into the `exec()` call. The `@` is preserved by the constructor regex, and the `substr`/`strrpos` extraction splits on `@` leaving `evil.com` as `$host`, but a crafted hostname portion with backticks or `$(...)` before the `@` could inject commands. Additionally, even without backticks, the unquoted `$host` in the shell command means spaces or other metas would be word-split.
impact: Medium -- requires the library to be used with attacker-controlled email input on a backend where `nslookup`/`dig` is available. If deployed in a web-facing validation endpoint, RCE is possible.
verify_steps: 1) Check if this library is required by any peoplefone web app or API (search composer.json/lock for `peoplefone/mail-validator-mx-server`). 2) If deployed, test with `attacker\`id\`@domain.tld` as email input and observe command output. 3) Check if the calling code sanitizes input before calling `setContact()`/`validate()`.
[HYP] Test file expects external credentials file with hardcoded fallback values
class: OTHER
asset: peoplefone/provisioning-rpc/tests/test.php:7-8
confidence: 20
reasoning: `tests/test.php` does `include_once __DIR__ . '/../../provisioning-rpc-settings.php'` — a file that is `.gitignore`d. If a developer accidentally commits this file to a different branch or fork, it would leak VoIP provisioning API credentials (Snom, Panasonic, Gigaset, Yealink, Auerswald accounts). The fallback values `['username', 'password']` are harmless placeholder strings, but the pattern itself is a credential-leak risk vector.
impact: Low -- the file is gitignored and not present in the repo. Risk is future accidental commit.
verify_steps: 1) Check all branches/tags for `provisioning-rpc-settings.php` via `git log --all -- 'provisioning-rpc-settings.php'`. 2) If found, extract and check if credentials are live on the hardcoded provisioning endpoints (`https://secure-provisioning.snom.com:8083`, `https://provisioning.e-connecting.net`, `https://prov.gigaset.net`, `https://api-dm.yealink.com:8443`, `https://provisioning.auerswald.de`).
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-07 06:08:17 UTC
class: OTHER
asset: provisioning-rpc/src/ProvisioningRPC.php:9
confidence: 35
reasoning: `ProvisioningRPC::connect($model, $login)` builds a class name as `get_class().'Device'.ucfirst(strtolower($model))` and instantiates it with `new $classname($login)`. The `$model` parameter is caller-controlled. While the namespace prefix (`Peoplefone\ProvisioningRPCDevice...`) limits exploitation to classes within that namespace, if the namespace prefix ever expands or autoload is misconfigured, this could allow unintended class instantiation. No concrete exploitation path exists in current code.
impact: LOW (design concern, no current exploit path)
verify_steps: Review all callers of `ProvisioningRPC::connect()` to confirm `$model` is never user-supplied without a whitelist. Check that no additional classes exist in the `Peoplefone` namespace that could be instantiated.
class: SSRF
asset: provisioning-rpc/src/ProvisioningRPCDevice*.php (all device implementations, `addPhone($mac, $url, ...)`)
confidence: 25
reasoning: The `$url` parameter in `addPhone()` is passed directly to third-party provisioning APIs (snom, yealink, panasonic, gigaset, auerswald) without any validation or sanitization in this library. If a consuming application passes user-controlled input to this parameter without validation, it could cause SSRF against those third-party APIs. However, this is a library -- the validation responsibility lies with the consuming application.
impact: LOW (library-level design; depends on consumer validation)
verify_steps: Identify all applications consuming this library. Check if `$url` is derived from user input. If so, verify URL allowlisting/ validation exists upstream.
class: MISCONFIG
asset: mail-validator-mx-server/src/peoplefone/mailValidatorMXServer.php:241-246
confidence: 20
reasoning: `getMXDomains()` calls `exec("nslookup -querytype=mx ".$host, $lines)` and `exec("dig mx ".$host." | grep -v '^;' | grep ".$host, $lines)`. The `$host` is extracted from the email address via `substr($user, strrpos($user,'@')+1)` and sanitized with `preg_replace("/[^a-z0-9\-\.]/", "", strtolower($host))`. The regex only allows `[a-z0-9\-\.]` which prevents shell metacharacter injection. This is effectively mitigated by the strict input validation.
impact: LOW (mitigated by strict regex sanitization)
verify_steps: Confirm the regex `/[^a-z0-9\-\.]/` is applied to all code paths reaching `exec()`. No bypass path exists given the character set restriction.
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-07 12:35:38 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-07 17:53:14 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-07 20:53:25 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-07 23:08:08 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-08 01:14:20 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-08 05:59:14 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-08 10:37:56 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-08 14:46:02 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-08 18:10:51 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-08 21:10:54 UTC
[HYP] No source-code audit performed
class: OTHER
asset: cands.txt
confidence: 100
reasoning: "no org candidates" — no peoplefone GmbH public GitHub repos were identified. Without candidate repos, there is nothing to clone or scan for secrets/hardcoded credentials.
impact: N/A
verify_steps: N/A — no findings to verify
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-08 23:25:18 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-09 01:31:24 UTC
[HYP] Command Injection via exec() with User-Derived Input
class: OTHER
asset: peoplefone/mail-validator-mx-server/src/peoplefone/mailValidatorMXServer.php:241-245
confidence: 65
reasoning: |
impact: LOW-MEDIUM
verify_steps: |
[HYP] Hardcoded External Provisioning API Endpoints (Information Disclosure)
class: MISCONFIG
asset: peoplefone/provisioning-rpc/src/ProvisioningRPCDevice*.php (5 files)
confidence: 90
reasoning: |
impact: LOW
verify_steps: |
class: OTHER
asset: peoplefone/provisioning-rpc/src/ProvisioningRPCXML.php:18-20 (+ 5 device classes)
confidence: 85
reasoning: |
impact: LOW
verify_steps: |
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-09 06:43:17 UTC
[HYP] Command Injection Risk via exec() in MX Lookup
class: OTHER
asset: peoplefone/mail-validator-mx-server/src/peoplefone/mailValidatorMXServer.php:241-246
confidence: 45
reasoning: The getMXDomains() method passes user-derived $host to exec() for nslookup/dig commands. Input sanitization via regex (/[^a-z0-9\-\.]/) strips most dangerous characters, but the pattern of shelling out with any user-influenced data is inherently risky. If sanitization is bypassed or refined, command injection becomes possible.
impact: Medium - Requires bypass of input sanitization; could lead to RCE if exploitable
verify_steps: 1) Check if the library is used in any web-facing application 2) Test with malformed domain inputs to verify sanitization effectiveness 3) Review any downstream consumers of this library
[HYP] Outdated PHP Version Requirement
class: MISCONFIG
asset: peoplefone/mail-validator-mx-server/composer.json:13
confidence: 90
reasoning: Requires "php": ">=5.3.0" - PHP 5.x reached end-of-life in 2018 and has known security vulnerabilities. This suggests the library may not be maintained with current security standards.
impact: Low - Does not directly indicate a vulnerability but suggests security posture may be lacking
verify_steps: 1) Check if this library is actively used in production systems 2) Verify if PHP 5.3 compatibility is actually needed
[HYP] Internal Developer Email Exposed
class: OTHER
asset: peoplefone/provisioning-rpc/composer.json:10
confidence: 100
reasoning: Developer email nicolas.urech@peoplefone.com is publicly exposed in package metadata. This is standard for open-source packages but provides reconnaissance value for social engineering.
impact: Low - Standard for open-source; minimal direct security impact
verify_steps: Verify this is the intended public contact for the package
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
