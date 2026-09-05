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
