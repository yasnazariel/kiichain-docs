# RegisterNewDevice

**Category:** System\
**Permissions:** Operator, Trading\
**Call Type:** Synchronous

**RegisterNewDevice** is the device register confirmation call. It will take the hashcode and validation code sent in an email to verify a device as trusted\*_RegisterNewDevice._\*

#### Request <a href="#request" id="request"></a>

```
{
    "HashCode": "",
    "PendingEmailCode": ""
}
```

| Key              | Value                                             |
| ---------------- | ------------------------------------------------- |
| HashCode         | **string.** Hash code associated with the device. |
| PendingEmailCode | **string.** Email code to register device         |

#### Response <a href="#response" id="response"></a>

```
{
    "result": true,
    "errormsg": "",
    "errorcode": 0,
    "detail": ""
}
```

The Response is a standard response object.

| Key       | Value                                                                                                                                                                                                                                                                                                                                                                                                       |
| --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| result    | **Boolean.** If the hash code and validation code have successfully verified a device, _result_ is _true;_ otherwise it is _false._                                                                                                                                                                                                                                                                         |
| errormsg  | <p><strong>string.</strong> A successful receipt of the call returns <em>null.</em> The <em>errormsg</em> key for an unsuccessful call returns one of the following messages:<br>Not Authorized (errorcode 20)<br>Invalid Response (errorcode 100)<br>Operation Failed (errorcode 101)<br>Server Error (errorcode 102)<br>Resource Not Found (errorcode 104)<br>Operation Not Supported (errorcode 106)</p> |
| errorcode | **integer.** A successful receipt of the call returns 0. An unsuccessful receipt of the call returns one of the _errorcodes_ shown in the _errormsg_ list.                                                                                                                                                                                                                                                  |
| detail    | **string.** Message text that the system may send.                                                                                                                                                                                                                                                                                                                                                          |
