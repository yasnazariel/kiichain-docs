# Standard Response Objects and Common Error Codes

A response to an API call usually consists of a specific response, but both successful and unsuccessful responses may consist of a generic response object that verifies only that the call was received, and not that the action requested by the call took place. A generic response to an unsuccessful call provides an error code. A generic response looks like Example 3.

#### Example 3 <a href="#example-3" id="example-3"></a>

> Example 3

```
{
    "result":true,
    "errormsg":"",
    "errorcode": 0,
    "detail":"",
}
```

| Key       | Value                                                                                                                                                                                                                                                                                                                                                            |
| --------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| result    | **Boolean.** If the call has been successfully received by the Order Management System, result is _true_; otherwise it is _false_.                                                                                                                                                                                                                               |
| errormsg  | <p><strong>string.</strong> A successful receipt of the call returns <em>null</em>. The <em>errormsg</em> key for an unsuccessful call returns one of the following messages:<br>Not Authorized (errorcode 20)<br>Invalid Response (errorcode 100)<br>Operation Failed (errorcode 101)<br>Server Error (errorcode 102)<br>Resource Not Found (errorcode 104)</p> |
| errorcode | **integer.** A successful receipt of the call returns 0. An unsuccessful receipt of the call returns one of the _errorcodes_ shown in the _errormsg_ list.                                                                                                                                                                                                       |
| detail    | **string.** Message text that the system may send. The content of this key is usually _null_.                                                                                                                                                                                                                                                                    |
