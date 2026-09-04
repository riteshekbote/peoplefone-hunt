
## 2026-09-02 21:54:06 UTC


## 2026-09-02 23:55:44 UTC


## 2026-09-03 03:38:09 UTC


## 2026-09-03 08:20:18 UTC


## 2026-09-03 13:01:56 UTC


## 2026-09-03 17:09:09 UTC
https://auth.peoplefone.com/.well-known/oauth-authorization-server -> HTTP 404
https://auth.peoplefone.com/oauth/authorize?client_id=test&redirect_uri=https://evil.com&response_type=code&scope=openid -> HTTP 404
https://api.peoplefone.com/.well-known/openid-configuration -> HTTP 404
https://api.peoplefone.com/api/v1/ -> HTTP 404
https://api.peoplefone.com/swagger.json -> HTTP 404
https://www.peoplefone.com/en-ch/developer -> 200 len=?
https://auth.peoplefone.com -> HTTP 404
https://support.peoplefone.com/che/willkommen/ -> 200 len=?

## 2026-09-03 19:45:39 UTC
https://auth.peoplefone.com/.well-known/oauth-authorization-server -> HTTP 404
https://auth.peoplefone.com/oauth/authorize?client_id=test&redirect_uri=https://evil.com&response_type=code&scope=openid -> HTTP 404
https://api.peoplefone.com/.well-known/openid-configuration -> HTTP 404
https://api.peoplefone.com/api/v1/ -> HTTP 404
https://api.peoplefone.com/swagger.json -> HTTP 404
https://www.peoplefone.com/en-ch/developer -> 200 len=?
https://www.peoplefone.com/en-ch/developer/graphql -> 200 len=?
https://auth.peoplefone.com -> HTTP 404
https://support.peoplefone.com/che/willkommen/ -> 200 len=?

## 2026-09-03 22:39:49 UTC
https://auth.peoplefone.com/oauth/authorize?client_id=1&redirect_uri=https://evil.com/callback&response_type=code&scope=openid&state=<captured_state -> HTTP 404
https://configuration-api.peoplefone.com/customer/voip/v1/virtualUsers/{other_tenant_id -> HTTP 401
https://call-api.peoplefone.com/customer/call-management/v1/call -> HTTP 401
https://auth.peoplefone.com/oauth/authorize?client_id=1&redirect_uri=https://attacker.com/callback&response_type=code&scope=openid&state=<fresh_state_from_portal_login -> HTTP 404
https://api.peoplefone.com/services/api-doc/ -> 200 len=?
https://auth.peoplefone.com -> HTTP 404

## 2026-09-04 00:31:55 UTC
https://api.peoplefone.com/services/api-doc/ -> 200 len=?
https://configuration-api.peoplefone.com/services/api-doc/ -> HTTP 404
