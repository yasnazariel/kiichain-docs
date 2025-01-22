# GetValidate2FARequiredEndpoints

**Category:** System\
**Permissions:** Public\
**Call Type:** Synchronous

Gets endpoints that require 2FA Validation

#### Request <a href="#request" id="request"></a>

```
{}
```

There is no payload.

#### Response <a href="#response" id="response"></a>

```
["createwithdrawticket", "createdepositticket", "adduserpermission"]
```

The response is a list of endpoints, all lowercase.
