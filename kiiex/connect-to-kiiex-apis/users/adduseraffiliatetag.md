# AddUserAffiliateTag

**Category:** User\
**Permissions:** Operator, Trading\
**Call Type:** Synchronous

Associates a user affiliate tag to a user. An affiliate tag allows a user to encourage others to join the exchange and provides a way to track those new members back to the initiating user.

#### Request <a href="#request" id="request"></a>

```
{
  "omsId":0,
  "userId":0,
  "affiliateId":0,
  "affiliateTag":""
}
```

| Key          | Value                                                                          |
| ------------ | ------------------------------------------------------------------------------ |
| omsId        | **integer.** The ID of the Order Management System on which the user operates. |
| userId       | **integer.** The user's ID.                                                    |
| affiliateId  | **integer.** The affiliate ID.                                                 |
| affiliateTag | **string.** The alphanumeric tag used to identify new affiliating members.     |

#### Response <a href="#response" id="response"></a>

```
{
  "result":true,
  "errormsg":"",
  "errorcode":0,
  "detail":""
}
```

| Key       | Value                                                                                                                                                                                                                                                                                                                       |
| --------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| result    | **Boolean.** _True_ signifies that the server has received the request to associate the affiliate tag with a specific user (not that it has done so); _false_ signifies an error.                                                                                                                                           |
| errormsg  | **string.** A successful response returns _null_; the _errormsg_ parameter for an unsuccessful response returns one of the following messages: Not Authorized (_errorcode_ 20), Invalid Request (_errorcode_ 100), Operation Failed (_errorcode_ 101), Server Error (_errorcode_ 102), Resource Not Found (_errorcode_ 104) |
| errorcode | **integer.** A successful response returns 0. An unsuccessful response returns one of the _errorcodes_ shown in the _errormsg_ list.                                                                                                                                                                                        |
| detail    | **string.** Message text that the system may send. Usually _null_.                                                                                                                                                                                                                                                          |
