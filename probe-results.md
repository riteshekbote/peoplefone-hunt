
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

## 2026-09-04 05:12:13 UTC
https://configuration-api.peoplefone.com/services/api-doc/ -> HTTP 404
https://api.peoplefone.com/services/api-doc/ -> 200 len=?
https://api.peoplefone.com/customer/sms/v1/sms/messages -> HTTP 401

## 2026-09-04 09:50:22 UTC
https://configuration-api.peoplefone.com/services/api-doc/ -> HTTP 404
https://api.peoplefone.com/services/api-doc/ -> 200 len=?

## 2026-09-04 14:21:19 UTC
https://configuration-api.peoplefone.com/services/api-doc/ -> HTTP 404
https://api.peoplefone.com/services/api-doc/ -> 200 len=?
https://api.peoplefone.com/services/api-doc/api/ -> HTTP 403

## 2026-09-04 17:48:51 UTC
https://configuration-api.peoplefone.com/services/api-doc/ -> HTTP 404
https://api.peoplefone.com/services/api-doc/ -> 200 len=?

## 2026-09-04 19:59:10 UTC
https://api.peoplefone.com/services/api-doc/ -> 200 len=?

## 2026-09-04 22:17:35 UTC
https://api.peoplefone.com/services/api-doc/ -> 200 len=?

## 2026-09-05 00:16:10 UTC
https://api.peoplefone.com/services/api-doc/ -> 200 len=?

## 2026-09-05 04:42:33 UTC
https://api.peoplefone.com/services/api-doc/ -> 200 len=?

## 2026-09-05 08:40:20 UTC
https://api.peoplefone.com/services/api-doc/ -> 200 len=?

## 2026-09-05 12:06:04 UTC
https://api.peoplefone.com/services/api-doc/ -> 200 len=?

## 2026-09-05 15:27:50 UTC
https://api.peoplefone.com/services/api-doc/ -> 200 len=?

## 2026-09-05 17:42:48 UTC
https://api.peoplefone.com/services/api-doc/ -> 200 len=?

## 2026-09-05 19:35:14 UTC
https://api.peoplefone.com/services/api-doc/ -> 200 len=?

## 2026-09-05 21:46:35 UTC
https://api.peoplefone.com/services/api-doc/ -> 200 len=?

## 2026-09-05 23:39:49 UTC
https://api.peoplefone.com/services/api-doc/ -> 200 len=?

## 2026-09-06 01:23:15 UTC
https://api.peoplefone.com/services/api-doc/ -> 200 len=?

## 2026-09-06 06:31:55 UTC
https://api.peoplefone.com/services/api-doc/ -> 200 len=?

## 2026-09-06 11:29:48 UTC
https://api.peoplefone.com/services/api-doc/ -> 200 len=?

## 2026-09-06 14:26:39 UTC
https://api.peoplefone.com/services/api-doc/ -> 200 len=?

## 2026-09-06 17:11:46 UTC
https://api.peoplefone.com/services/api-doc/ -> 200 len=?

## 2026-09-06 19:31:07 UTC
https://api.peoplefone.com/services/api-doc/ -> 200 len=?

## 2026-09-06 21:30:16 UTC
https://api.peoplefone.com/services/api-doc/ -> 200 len=?

## 2026-09-06 23:10:56 UTC
https://api.peoplefone.com/services/api-doc/ -> 200 len=?

## 2026-09-07 01:12:41 UTC
https://api.peoplefone.com/services/api-doc/ -> 200 len=?

## 2026-09-07 06:14:31 UTC
https://api.peoplefone.com/services/api-doc/ -> 200 len=?

## 2026-09-07 12:47:48 UTC
https://api.peoplefone.com/services/api-doc/ -> 200 len=?

## 2026-09-07 18:15:46 UTC
https://api.peoplefone.com/services/api-doc/ -> 200 len=?

## 2026-09-07 21:43:20 UTC
https://api.peoplefone.com/services/api-doc/ -> 200 len=?
https://auth.peoplefone.com/de_CH/register -> HTTP 500
https://call-api.peoplefone.com/services/api-doc/ -> HTTP 404

## 2026-09-07 23:49:17 UTC
https://api.peoplefone.com/services/api-doc/ -> 200 len=?

## 2026-09-08 03:46:51 UTC
https://api.peoplefone.com/services/api-doc/ -> 200 len=?

## 2026-09-08 09:03:31 UTC


## 2026-09-08 13:30:00 UTC
https://api.peoplefone.com/services/api-doc/ -> 200 len=?

## 2026-09-08 17:47:47 UTC
https://api.peoplefone.com/services/api-doc/ -> 200 len=?

## 2026-09-08 20:17:46 UTC
https://api.peoplefone.com/services/api-doc/ -> 200 len=?

## 2026-09-08 22:46:24 UTC
https://api.peoplefone.com/services/api-doc/ -> 200 len=?

## 2026-09-09 01:13:47 UTC
https://api.peoplefone.com/services/api-doc/ -> 200 len=?

## 2026-09-09 06:11:16 UTC
https://api.peoplefone.com/services/api-doc/ -> 200 len=?

## 2026-09-09 11:42:24 UTC
https://api.peoplefone.com/services/api-doc/ -> 200 len=?

## 2026-09-09 15:26:47 UTC
https://api.peoplefone.com/services/api-doc/ -> 200 len=?

## 2026-09-09 18:45:54 UTC
https://api.peoplefone.com/services/api-doc/ -> 200 len=?

## 2026-09-09 21:36:47 UTC
https://api.peoplefone.com/services/api-doc/ -> 200 len=?

## 2026-09-09 23:33:21 UTC


## 2026-09-10 01:31:31 UTC
https://api.peoplefone.com/services/api-doc/ -> 200 len=?

## 2026-09-10 06:43:47 UTC
https://api.peoplefone.com/services/api-doc/ -> 200 len=?
