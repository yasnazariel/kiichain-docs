# UpdateUserAffiliateTag

**Category:** User\
**Permissions:** Operator, Trading\
**Call Type:** Synchronous

Updates the user affiliate tag with new or revised information. An affiliate tag allows a user to encourage others to join the exchange and provides a way to track those new members back to the initiating user.

#### Request <a href="#request" id="request"></a>

```
{
    "omsId":0,
    "userId":0,
    "affiliateId":0,
    "affiliateTag":""
}
```

| Key          | Value                                                                                                |
| ------------ | ---------------------------------------------------------------------------------------------------- |
| omsId        | **integer.** The ID of the Order Management System on which the user and his affiliate tag operates. |
| userId       | **integer.** The ID of the user whose affiliate tag you are modifying.                               |
| affiliateId  | **integer.** The ID of the affiliate.                                                                |
| affiliateTag | **string.** The alphanumeric tag used to identify new affiliating members.                           |

#### Response <a href="#response" id="response"></a>

```
{
  "result":true,
  "errormsg":"",
  "errorcode":0,
  "detail":""
 }
```

| Key       | Value                                                                                                                                                                                                                                                                                                                                                                                   |
| --------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| result    | **Boolean.** A successful receipt of the unsubscribe request returns _true_; and unsuccessful receipt (an error condition) returns _false_.                                                                                                                                                                                                                                             |
| errormsg  | <p><strong>string.</strong> A successful receipt of the unsubscribe request returns <em>null</em>; the <em>errormsg</em> parameter for an unsuccessful request returns one of the following messages:<br>Not Authorized (errorcode 20)<br>Invalid Request (errorcode 100)<br>Operation Failed (errorcode 101)<br>Server Error (errorcode 102)<br>Resource Not Found (errorcode 104)</p> |
| errorcode | **integer.** A successful receipt of the unsubscribe request returns 0. An unsuccessful receipt returns one of the _errorcodes_ shown in the _errormsg_ list.                                                                                                                                                                                                                           |
| detail    | **string.** Message text that the system may send. Usually _null_.                                                                                                                                                                                                                                                                                                                      |
