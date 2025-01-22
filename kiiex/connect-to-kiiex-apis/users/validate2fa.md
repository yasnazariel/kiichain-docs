# Validate2FA

**Category:** System\
**Permissions:**\
**Call Type:** Synchronous

Validate 2FA to get access to the 2FA required endpoints

#### Request <a href="#request" id="request"></a>

```
{
    "TFaType":"TFATYPE",
    "Code": "YourCode"
}
```

| Key     | Value                              |
| ------- | ---------------------------------- |
| TFaType | **string.** Type of authentication |
| Code    | **string.** Authentication code    |

#### Response <a href="#response" id="response"></a>

```
{
    "TFaAuthenticated": true
}
```

| Key              | Value                                                        |
| ---------------- | ------------------------------------------------------------ |
| TFaAuthenticated | **Boolean.** If authenticatation is successful, returns true |
