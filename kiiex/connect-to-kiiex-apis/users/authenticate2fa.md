# Authenticate2FA

**Category:** Authentication\
**Permissions:** Public\
**Call Type:** Synchronous

#### Request <a href="#request" id="request"></a>

```
{
  "Code": "YourCode"
}
```

Completes the second part of a two-factor authentication by sending the authentication token from the non-KIIEX authentication system to the Order Management System. The call returns a verification that the user logging in has been authenticated, and a token.

Here is how the two-factor authentication process works:

1. Call **webauthenticateuser**. The response includes values for _TwoFAType_ and _TwoFAToken_. For example, _TwoFAType_ may return "Google," and the _TwoFAToken_ then returns a Google-appropriate token (which in this case would be a QR code).
2. Enter the _TwoFAToken_ into the two-factor authentication program, for example, Google Authenticator. The authentication program returns a different token.
3. Call **authenticate2FA** with the token you received from the two-factor authentication program (shown as _YourCode_ in the Request example below).

| Key  | Value                                                                             |
| ---- | --------------------------------------------------------------------------------- |
| Code | **string**. _Code_ holds the token obtained from the other authentication source. |

#### Response <a href="#response" id="response"></a>

```
{
  "Authenticated": true,
  "SessionToken": "YourSessionToken"
}
```

| Key           | Value                                                                                                                                                                                                                                                                                                                                                       |
| ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Authenticated | **Boolean**. A successful authentication returns _true_. Unsuccessful returns _false_.                                                                                                                                                                                                                                                                      |
| SessionToken  | **string**. The _SessionToken_ is valid during the current session for connections from the same IP address. If the connection is interrupted during the session, you can sign back in using the _SessionToken_ instead of repeating the full two-factor authentication process. A session lasts one hour after the last-detected activity or until logout. |

> To send a session token to re-establish an interrupted session:

```
{
  "SessionToken": "YourSessionToken"
}
```
