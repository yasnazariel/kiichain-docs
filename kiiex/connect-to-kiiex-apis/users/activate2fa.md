# Activate2FA

**Category:** Activation\
**Permissions:** Public\
**Call Type:** Synchronous

#### Request <a href="#request" id="request"></a>

```
{
  "Code":"YourCode"
}
```

Completes the second half of a two-factor authentication by sending the 2FA code while registering for the exchange.

| Key  | Value                                                              |
| ---- | ------------------------------------------------------------------ |
| Code | **string.** The alphanumeric code you received for authentication. |

#### Response <a href="#response" id="response"></a>

```
{
  "Activated": true,
  "Error":"ErrorMessage"
}
```

| Key       | Value                                                                   |
| --------- | ----------------------------------------------------------------------- |
| Activated | **Boolean.** _True_ if the activation code is accepted; _false_ if not. |
| Error     | **string.** Error message from the server.                              |
