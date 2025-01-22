# LogOut

**Category:** Authentication\
**Permissions:** Public\
**Call Type:** Synchronous

**LogOut** ends the current websocket session.

#### Request <a href="#request" id="request"></a>

There is no payload for a **LogOut** request.

```
{ }
```

#### Response <a href="#response" id="response"></a>

```
{
  "result":true,
  "errormsg":null,
  "errorcode":0,
  "detail":null
}
```

| Key       | Value                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| --------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| result    | **Boolean**. A successful logout returns _true_; an unsuccessful logout (an error condition) returns _false_.                                                                                                                                                                                                                                                                                                                                      |
| errormsg  | <p><strong>string</strong>. A successful logout returns null; the <em>errormsg</em> parameter for an unsuccessful logout returns one of the following messages:<br>Not Authorized (errorcode 20)<br>Invalid Response (errorcode 100)<br>Operation Failed (errorcode 101)<br>Server Error (errorcode 102)<br>Resource Not Found (errorcode 104)<br><br>Not Authorized and Resource Not Found are unlikely errors for a <strong>LogOut</strong>.</p> |
| errorcode | **integer**. A successful logout returns _0_. An unsuccessful logout returns one of the errorcodes shown in the _errormsg_ list.                                                                                                                                                                                                                                                                                                                   |
| detail    | **string**. Message text that the system may send. Usually _null_.                                                                                                                                                                                                                                                                                                                                                                                 |
