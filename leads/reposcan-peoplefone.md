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
## REPOSCAN 2026-09-09 11:51:27 UTC
[HYP] Command Injection Risk via exec() with User-Derived Input
class: SSRF
asset: peoplefone/mail-validator-mx-server/src/peoplefone/mailValidatorMXServer.php:242-246
confidence: 70
reasoning: getMXDomains() extracts domain from user-supplied email, sanitizes with regex /[a-z0-9\-\.]/, then passes $host into exec("nslookup -querytype=mx ".$host) and exec("dig mx ".$host." | grep ..."). While the regex strips most shell metacharacters, the pattern of shelling out with user-influenced data is inherently risky. If sanitization is bypassed or refined, command injection becomes possible.
impact: Medium - Requires bypass of input sanitization; could lead to RCE if exploitable
verify_steps: 1) Check if the library is used in any web-facing application 2) Test with malformed domain inputs to verify sanitization effectiveness 3) Review any downstream consumers of this library
[HYP] SSRF via Unvalidated MX Server Connection
class: SSRF
asset: peoplefone/mail-validator-mx-server/src/peoplefone/mailValidatorMXServer.php:274
confidence: 60
reasoning: getMXConnection() calls fsockopen($host, $this->sock_port, ...) where $host comes from DNS MX lookup results. No IP range validation or allowlist is performed. An attacker who controls DNS for a domain can point MX records to internal/private IPs (RFC 1918, link-local, cloud metadata endpoints). The connection is outbound SMTP on port 25.
impact: Medium - Could lead to SSRF against internal services if deployed on cloud infrastructure
verify_steps: 1) Create a domain with MX record pointing to 169.254.169.254 (AWS metadata) 2) Use mailValidatorMXServer to validate an email on that domain 3) Observe connection attempt to the metadata endpoint
[HYP] Incomplete .gitignore - Credential File Not Excluded
class: MISCONFIG
asset: peoplefone/provisioning-rpc/.gitignore
confidence: 90
reasoning: The .gitignore does NOT explicitly exclude provisioning-rpc-settings.php (referenced in tests/test.php via file_exists). If this settings file were ever committed, it would contain real credentials ($auerswald_login, $gigaset_login, etc.) for third-party provisioning APIs. Currently the file is not committed, but the incomplete .gitignore creates risk of accidental credential exposure.
impact: Low - No current leak, but design flaw could lead to future credential exposure
verify_steps: 1) Check all branches/tags for provisioning-rpc-settings.php via git log --all -- 'provisioning-rpc-settings.php' 2) Add provisioning-rpc-settings.php to .gitignore to prevent accidental commit
[HYP] Error Message Leakage via die()
class: OTHER
asset: peoplefone/provisioning-rpc/src/ProvisioningRPC.php:17
confidence: 85
reasoning: The catch block uses die($t->getMessage()) which leaks exception strings to output. While not a direct vulnerability, this could expose internal error details or stack information in production environments.
impact: Low - Information disclosure via error messages
verify_steps: 1) Confirm error handling is not exposed to end users 2) Check if error output is logged to files accessible by unauthorized parties
[HYP] Hardcoded Third-Party Provisioning API Endpoints
class: OTHER
asset: peoplefone/provisioning-rpc/src/ProvisioningRPCDevice{Auerswald,Gigaset,Panasonic,Snom,Yealink}.php
confidence: 90
reasoning: Five device classes contain hardcoded base URIs for external vendor provisioning APIs: https://secure-provisioning.snom.com:8083, https://prov.gigaset.net, https://api-dm.yealink.com:8443, https://provisioning.auerswald.de, https://provisioning.e-connecting.net. These are third-party phone vendor endpoints, not peoplefone infrastructure. The constructor default parameter $client_auth=['username','password'] is a placeholder, not a real credential.
impact: Low (third-party public endpoints; no live credentials leaked)
verify_steps: 1) Confirm these endpoints are still live/vendor-operated 2) Verify provisioning-rpc-settings.php is never committed in any branch/commit history
[HYP] Developer Email Exposed in Package Metadata
class: OTHER
asset: peoplefone/provisioning-rpc/composer.json:10
confidence: 100
reasoning: Developer email nicolas.urech@peoplefone.com is publicly exposed in package metadata. This is standard for open-source packages but provides reconnaissance value for social engineering.
impact: Low - Standard for open-source; minimal direct security impact
verify_steps: Verify this is the intended public contact for the package
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-09 15:29:52 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-09 18:50:03 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-09 21:22:53 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-09 23:29:14 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-10 01:24:14 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-10 06:39:31 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-10 11:46:22 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-10 15:24:23 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-10 18:40:16 UTC
[HYP] No in-scope repositories available for audit
class: OTHER
asset: N/A
confidence: 100
reasoning: User specified "no org candidates". GitHub API confirms no public org named "peoplefone" exists. No repos to clone or grep.
impact: None (audit cannot proceed)
verify_steps: N/A
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-10 21:11:16 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-10 23:11:50 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-11 01:07:06 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-11 06:02:43 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-11 11:23:23 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-11 15:10:53 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-11 18:35:55 UTC
[HYP] Command Injection via exec() on unsanitized user input
class: OTHER
asset: mail-validator-mx-server/src/peoplefone/mailValidatorMXServer.php:242-245
confidence: 60
reasoning: The getMXDomains() method extracts a hostname from user-supplied email addresses and passes it directly to exec("nslookup -querytype=mx ".$host) and exec("dig mx ".$host." | grep -v '^;' | grep ".$host). Although there is a regex filter [^a-z0-9\-\.] applied to $host earlier (line 239), the filtering occurs before the exec call but after the variable is extracted from the user email. The regex strips most shell metacharacters, which reduces but does not fully eliminate injection risk (e.g., backtick or $() within the regex allowance is not clear). The code pattern is inherently dangerous.
impact: Medium — if regex is bypassed or modified, arbitrary command execution on the host.
verify_steps: 1. Confirm whether the regex at line 239 truly strips all shell metacharacters (backtick, $(), semicolons, pipes). 2. Verify if this library is used in any web-facing application in the peoplefone stack (check internal repos, Packagist download stats, or internal dependency manifests). 3. Check if any web endpoint passes user-controlled email input into this class.
[HYP] SSRF via SMTP connection to attacker-controlled MX host
class: SSRF
asset: mail-validator-mx-server/src/peoplefone/mailValidatorMXServer.php:266-286
confidence: 45
reasoning: The getMXConnection() method takes an array of DNS-resolved MX hosts and opens a direct fsockopen() connection to each. An attacker-controlled domain could resolve to an internal IP (127.0.0.1, 10.x, 192.168.x), making this an SSRF vector to reach internal services via SMTP on port 25. The email address is user-supplied (setContact), and the MX lookup is DNS-based. No validation is performed on the resolved IP to prevent internal network scanning.
impact: Medium — internal network scanning or interaction with internal SMTP services if the library is deployed in a web context.
verify_steps: 1. Verify if this library is used behind any HTTP endpoint (web app, API). 2. Check if any callers of setContact() accept untrusted input. 3. Confirm whether DNS resolution for MX records could return RFC1918 addresses in the deployment environment.
[HYP] Default credentials placeholder in constructor signatures
class: OTHER
asset: provisioning-rpc/src/ProvisioningRPCDevice{Snom,Panasonic,Gigaset,Auerswald,Yealink}.php:24/14/15/14/14
confidence: 20
reasoning: All five device classes have constructor default parameters: array $client_auth=['username','password']. These are literal string array defaults, not actual leaked credentials. However, they indicate the auth pattern (username/password basic auth) used for provisioning RPC calls to third-party VoIP APIs (snom, Panasonic, Gigaset, Auerswald, Yealink). If any consumer forgets to override the defaults, it would attempt authentication with literal "username"/"password" against live provisioning endpoints.
impact: Low — these are placeholder defaults in open-source library code, not real secrets. Risk is only if a consumer fails to provide credentials.
verify_steps: 1. Check if any downstream project instantiates these classes without overriding the default auth array. 2. Confirm these are not
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-11 21:13:56 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-11 23:18:23 UTC
class: MISCONFIG
asset: peoplefone/provisioning-rpc/tests/test.php:7-9
confidence: 55
reasoning: Test file attempts to include `provisioning-rpc-settings.php` from the parent directory, but `.gitignore` only excludes `vendor`, `composer.lock`, and `.idea`. If a developer creates this file with real provisioning API credentials (username/password pairs for Snom, Panasonic, Gigaset, Auerswald, Yealink) and commits without adding it to `.gitignore`, credentials would leak to the public repo.
impact: Medium — credential leakage if misconfigured
verify_steps: Check git history for any committed `provisioning-rpc-settings.php` or similar credential files; confirm the file is not tracked via `git ls-files`.
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-12 01:12:20 UTC
class: OTHER
asset: `peoplefone/mail-validator-mx-server/src/peoplefone/mailValidatorMXServer.php:242-245`
confidence: 15
reasoning: `$host` is derived from the email domain (line 238-239) and stripped to `[a-z0-9\-\.]` via `preg_replace` on line 239. The sanitized value is then interpolated into `exec("nslookup -querytype=mx ".$host)` and `exec("dig mx ".$host." | grep ...")`. The regex is restrictive enough to prevent shell metacharacter injection in practice, making this **low-confidence** — it is a defense-in-depth concern rather than an exploitable finding. No live in-scope peoplefone deployment was confirmed running this code.
impact: informational
verify_steps: Check if `mail-validator-mx-server` is deployed anywhere on peoplefone infrastructure (DNS records, package registries). The regex sanitization appears sufficient to block injection.
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-12 05:48:58 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-12 09:44:21 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-12 13:13:01 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-12 16:19:43 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-12 18:29:34 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-12 21:00:40 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-12 22:43:38 UTC
[HYP] Command injection surface in mail-validator-mx-server
class: OTHER
asset: peoplefone/mail-validator-mx-server/src/peoplefone/mailValidatorMXServer.php:241-245
confidence: 15
reasoning: exec() calls with $host variable (nslookup/dig). However, input is sanitized via regex `[^a-z0-9\-\.]` on line 239 before the exec, which strips all shell metacharacters. Not exploitable as-is.
impact: Informational
verify_steps: N/A - not actionable
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-13 00:29:28 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-13 05:23:14 UTC
class: MISCONFIG
asset: peoplefone/mail-validator-mx-server → src/peoplefone/mailValidatorMXServer.php:242-245
confidence: 30
reasoning: |
impact: Medium — latent command injection; mitigated by regex but violates secure coding
verify_steps: |
class: MISCONFIG
asset: peoplefone/provisioning-rpc → .gitignore (absent entry)
confidence: 25
reasoning: |
impact: Low — procedural risk, no current credential exposure
verify_steps: |
class: MISCONFIG
asset: gido/slackphones → index.js:19-20
confidence: 45
reasoning: |
impact: Low — information disclosure of internal URL structure
verify_steps: |
class: SSRF
asset: gido/slackphones → index.js:113,65,95
confidence: 40
reasoning: |
impact: Medium — server-side request forgery if SLACK_TOKEN is compromised
verify_steps: |
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-13 10:21:39 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-13 14:38:19 UTC
[HYP] <none> — No repos found to audit
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-13 17:37:43 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-13 19:44:34 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-13 21:55:06 UTC
[HYP] No findings
class: N/A
asset: peoplefone/provisioning-rpc, peoplefone/mail-validator-mx-server
confidence: 0
reasoning: Both repos are public Composer client libraries. No hardcoded secrets, no server-side endpoints, no user-input-driven URL construction, no JWT/auth logic. Test files use placeholder ['username','password'] defaults only.
impact: None
verify_steps: N/A — no findings to verify
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-13 23:44:40 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-14 02:08:06 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-14 07:55:02 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-14 14:32:02 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-14 19:34:05 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-14 22:43:37 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-15 01:03:57 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-15 06:10:54 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-15 11:45:47 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-15 15:50:46 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-15 19:22:41 UTC
[HYP] Command Injection via exec() in MX Validator
class: OTHER
asset: peoplefone/mail-validator-mx-server/src/peoplefone/mailValidatorMXServer.php:242,245
confidence: 35
reasoning: getMXDomains() passes $host (derived from user-supplied email address) into exec("nslookup -querytype=mx ".$host) and exec("dig mx ".$host." | grep -v '^;' | grep ".$host). The $host is sanitized at line 239 via preg_replace("/[^a-z0-9\-\.]/", "", ...) which strips shell metacharacters, making classic command injection impractical. However, if this class is ever used in a context where the regex is bypassed or modified (e.g., subclass override, different PHP version PCRE behavior), the exec() calls become exploitable. The grep ".$host on line 245 also passes unsanitized $host as a regex argument (dots in domains match any character — minor logic flaw).
impact: low
verify_steps: 1) Check if this class is instantiated in any web-facing application in peoplefone's stack where email input comes from HTTP requests. 2) Confirm whether the regex sanitization at line 239 is always applied before exec(). 3) Test if a crafted domain like "x;id" could survive the regex (it cannot with current filter — low confidence).
[HYP] Error Message Disclosure via die() in ProvisioningRPC Factory
class: OTHER
asset: peoplefone/provisioning-rpc/src/ProvisioningRPC.php:17
confidence: 50
reasoning: ProvisioningRPC::connect() catches Throwable and calls die($t->getMessage().PHP_EOL). If an invalid $model string is passed that fails class instantiation, the full exception message (which may include file paths, class names, or PHP internal error details) is printed to output and execution terminates. This is out-of-scope per program rules ("Descriptive error messages or headers"), but the die() itself is a poor practice in a library context — any consumer calling this with an unsupported manufacturer gets a hard crash with verbose error.
impact: informational
verify_steps: 1) Confirm this library is used in a web context where die() output is visible to end users. 2) Verify whether any web application wraps this call and suppresses output.
[HYP] Hardcoded Third-Party Provisioning API Endpoints
class: MISCONFIG
asset: peoplefone/provisioning-rpc/src/ProvisioningRPCDevice*.php (5 files)
confidence: 25
reasoning: Five device classes hardcode vendor XML-RPC API endpoints: secure-provisioning.snom.com:8083 (line 7), provisioning.e-connecting.net (line 7), prov.gigaset.net (line 7), provisioning.auerswald.de (line 7), api-dm.yealink.com:8443 (line 7). These are third-party vendor endpoints (not peoplefone's own infra) and their URLs are publicly documented by each vendor. No credentials are hardcoded — auth is passed at runtime. These reveal the specific vendor provisioning APIs peoplefone integrates with, which is low-sensitivity infrastructure reconnaissance info.
impact: informational
verify_steps: 1) Confirm these are indeed public vendor endpoints (check vendor documentation). 2) Determine if any of these endpoints have been deprecated or have known vulnerabilities.
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-15 22:26:12 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-16 00:45:28 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-16 05:27:49 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-16 10:15:51 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-16 15:02:25 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-16 18:44:12 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-16 21:47:36 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-16 23:57:09 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-17 02:53:10 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-17 08:06:55 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-17 13:29:26 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-17 17:43:58 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-17 20:41:39 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-17 23:13:18 UTC
[HYP] <none>
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-18 01:18:31 UTC
class: OTHER
asset: `peoplefone/mail-validator-mx-server/src/peoplefone/mailValidatorMXServer.php:242-245`
confidence: 30
reasoning: `getMXDomains()` extracts the domain from a user-supplied email, passes it through `preg_replace("/[^a-z0-9\-\.]/", "", ...)`, then feeds it to `exec("nslookup -querytype=mx ".$host)` and `exec("dig mx ".$host." | grep ...")`. The regex strips all shell metacharacters (`;|&`$\`` etc.), making injection impractical. However, `exec()` with externally-influenced input is a security anti-pattern; a regex bypass (e.g., encoding edge-case) would yield OS command injection.
impact: Low — effectively mitigated by regex; non-exploitable in current form
verify_steps: Confirm no upstream caller passes pre-sanitized input that could reintroduce metacharacters; verify PHP `escapeshellarg()` is not used elsewhere (it is not — defense-in-depth absent)
class: SSRF
asset: `peoplefone/provisioning-rpc/src/ProvisioningRPCDevice{Snom,Panasonic,Gigaset,Auerswald,Yealink}.php` — `addPhone(string $mac, string $url)`
confidence: 25
reasoning: All five device classes accept an arbitrary `$url` parameter and pass it directly to vendor XML-RPC APIs (e.g., `redirect.registerPhone`, `autoprov.registerDevice`, `DeviceRegister`) without any URL validation or allowlisting. If the calling application passes attacker-controlled input to this parameter, phones could be redirected to malicious provisioning servers (phone provision MITM). This is a caller-side issue, not a direct SSRF on the library server.
impact: Low — depends entirely on caller validation; library alone does not expose a server-side request
verify_steps: Identify all production consumers of `ProvisioningRPC::connect()->addPhone()` and verify they validate/allowlist the `$url` parameter before passing it
class: OTHER
asset: `peoplefone/provisioning-rpc/src/ProvisioningRPCDevice{Snom,Panasonic,Gigaset,Auerswald,Yealink}.php:14-24`
confidence: 5
reasoning: All five device classes define `__construct(array $client_auth=['username','password'])` with string-literal placeholder defaults. These are not real credentials — they are scaffolding defaults for documentation purposes. No real secrets are present. However, this pattern risks accidental credential leakage if a caller forgets to override and commits the default.
impact: Informational — no real secrets leaked; purely a code hygiene concern
verify_steps: Confirm no production code instantiates these classes without overriding the default `$client_auth`
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-18 05:59:14 UTC
[HYP] No in-scope public repositories found
class: OTHER
asset: github.com/peoplefone (non-existent)
confidence: 100
reasoning: The peoplefone GmbH GitHub organization does not exist as a public entity. The
impact: None — nothing to audit.
verify_steps: Visit https://github.com/peoplefone → 404. No public codebase to clone or scan.
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-18 10:32:28 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-18 14:37:38 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-18 17:56:06 UTC
[HYP] OS Command Injection via unsanitized hostname in exec()
class: OTHER
asset: peoplefone/mail-validator-mx-server/src/peoplefone/mailValidatorMXServer.php:242-245
confidence: 65
reasoning: In `getMXDomains()`, the `$host` variable (derived from an email address's domain portion) is passed directly into `exec("nslookup -querytype=mx ".$host)` and `exec("dig mx ".$host." | grep ...")` via string interpolation. Although a regex filter (`/[^a-z0-9\-\.]/`) strips most characters from `$host`, the `$user` parameter accepted by `setContact()` is only filtered with `/[^a-z0-9\-\.\@]/` and then the domain is extracted via `substr($user, strrpos($user,'@')+1)`. The regex applied to the domain in `getMXDomains()` is `/[^a-z0-9\-\.]/` which strips semicolons and pipes, making actual shell injection difficult. However, the pattern of interpolating external input into `exec()` is inherently unsafe — any future change to the regex or host extraction logic could immediately open a command injection vector. Additionally, backtick execution (`which nslookup`) on line 241 uses the same pattern.
impact: Medium — current regex mitigates direct exploitation, but the insecure pattern is live code and fragile to future modifications
verify_steps: Passive: Read `src/peoplefone/mailValidatorMXServer.php` lines 230-250. Confirm `exec()` receives string-interpolated `$host`. Confirm `$host` regex does not block all shell metacharacters. Active (if in scope): Craft an email domain with characters surviving the regex to test RCE.
[HYP] SSRF potential via fsockopen to user-influenced MX hosts
class: SSRF
asset: peoplefone/mail-validator-mx-server/src/peoplefone/mailValidatorMXServer.php:274
confidence: 45
reasoning: `getMXConnections()` calls `fsockopen($host, ...)` where `$host` is resolved from the MX lookup of an email domain. If an attacker controls DNS for a target domain (or the email validation is used server-side with attacker-supplied addresses), they could point MX records to an internal host and cause the server to open TCP connections to arbitrary internal services (port 25 default, but configurable via `setConnectionPort()`). The current usage in `tests/test.php` only validates well-known public domains, limiting real-world impact for this specific library.
impact: Low — requires the library to be used in a server-side context with attacker-controlled input and DNS control; default port is 25 (SMTP), not HTTP
verify_steps: Passive: Read `src/peoplefone/mailValidatorMXServer.php` lines 260-280. Confirm `fsockopen()` target is derived from MX lookup. Active: Register a domain, set MX to an internal IP, pass an email address on that domain to `setContact()`.
[HYP] die() with exception message on connection failure (information disclosure / unavailability)
class: OTHER
asset: peoplefone/provisioning-rpc/src/ProvisioningRPC.php:17
confidence: 30
reasoning: `ProvisioningRPC::connect()` wraps the device instantiation in a try/catch and calls `die($t->getMessage().PHP_EOL)` on any exception. This terminates the entire process and leaks the internal exception message (which could contain class names, connection details, or stack info depending on the underlying error). In a web context, this would cause a 500 error with potentially sensitive diagnostic info. The message itself comes from PHP class autoloading or constructor failures — no actual credentials are exposed in the current code.
impact: Low — only triggers if an invalid manufacturer name is passed; information leak is limited to PHP error messages
verify_steps: Passive: Read `src/ProvisioningRPC.php` line 17. Confirm `die()` is called with `$t->getMessage()`. Verify no credential data flows through the exception path.
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-18 20:06:16 UTC
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
## REPOSCAN 2026-09-18 22:37:41 UTC
[HYP] SSRF via fsockopen to attacker-controlled MX host
class: SSRF
asset: peoplefone/mail-validator-mx-server/src/peoplefone/mailValidatorMXServer.php:266-286
confidence: 60
reasoning: getMXConnection() calls fsockopen($host, $this->sock_port, ...) where $host is
impact: Medium
verify_steps: 1) Identify any peoplefone web app or API that instantiates
[HYP] exec() with user-derived input in MX lookup
class: MISCONFIG
asset: peoplefone/mail-validator-mx-server/src/peoplefone/mailValidatorMXServer.php:241-245
confidence: 45
reasoning: getMXDomains() passes $host (extracted from user-supplied email domain) into
impact: Low (mitigated by regex; defense-in-depth concern)
verify_steps: 1) Confirm regex at line 239 is always applied before exec(). 2) Verify no
[HYP] Incomplete .gitignore — credential file not excluded
class: MISCONFIG
asset: peoplefone/provisioning-rpc/.gitignore
confidence: 80
reasoning: tests/test.php (line 7-8) includes provisioning-rpc-settings.php via
impact: Low (no current leak; procedural risk)
verify_steps: 1) Run `git log --all -- 'provisioning-rpc-settings.php'` across all
[HYP] die() with exception message — information disclosure
class: OTHER
asset: peoplefone/provisioning-rpc/src/ProvisioningRPC.php:17
confidence: 50
reasoning: ProvisioningRPC::connect() catches Throwable and calls die($t->getMessage()).
impact: Informational (out of scope per program rules)
verify_steps: 1) Check if any peoplefone web app wraps this call and suppresses output.
TARGET_ORG not configured for peoplefone; skipping public-org deep scan.
