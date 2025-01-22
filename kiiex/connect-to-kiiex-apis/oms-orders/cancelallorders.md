# CancelAllOrders

**Category:** User\
**Permissions:** Operator, Trading\
**Call Type:** Synchronous

Cancels all open matching orders for the specified account on an Order Management System.

A user with Trading permission can cancel orders for himself; a user with Operator permissions can cancel orders for any account, instrument, or user.

**Warning:** **CancelAllOrders** will cancel all existing orders on an OMS when sending AccountID = 0 or when AccountID is ommited.**Note:** Multiple users may have access to the same account.

#### Request <a href="#request" id="request"></a>

```
{
  "AccountId": 0,
  "OMSId": 0
}
```

| Key       | Value                                                                                       |
| --------- | ------------------------------------------------------------------------------------------- |
| AccountId | **integer.** The account for which all orders are being canceled. _Conditionally optional._ |
| OMSId     | **integer.** The Order Management System under which the account operates. _Required_.      |

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
| result    | **Boolean.** If the call has been successfully received by the Order Management System, _result_ is _true;_ otherwise it is _false._                                                                                                                                                                                                                                                                        |
| errormsg  | <p><strong>string.</strong> A successful receipt of the call returns <em>null.</em> The <em>errormsg</em> key for an unsuccessful call returns one of the following messages:<br>Not Authorized (errorcode 20)<br>Invalid Response (errorcode 100)<br>Operation Failed (errorcode 101)<br>Server Error (errorcode 102)<br>Resource Not Found (errorcode 104)<br>Operation Not Supported (errorcode 106)</p> |
| errorcode | **integer.** A successful receipt of the call returns 0. An unsuccessful receipt of the call returns one of the _errorcodes_ shown in the _errormsg_ list.                                                                                                                                                                                                                                                  |
| detail    | **string.** Message text that the system may send.                                                                                                                                                                                                                                                                                                                                                          |

