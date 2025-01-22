# CancelWithdraw

**Category:** System\
**Permissions:** Withdraw\
**Call Type:** Synchronous

Cancels a pending withdrawal.

Only users with Withdraw permission can cancel their own pending withdrawals. An admin (a user with Operator permission) may cancel a withdraw, but is more likely to reject a withdraw.

#### Request <a href="#request" id="request"></a>

```
{
    "OMSId": 1,
    "UserId": 1,
    "AccountId": 1,
    "RequestCode": "Request Code GUID"
}
```

| Key         | Value                                                                                                                                                                                                                                                                                                                                                          |
| ----------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| OMSId       | **integer.** The ID of the Order Management System where the original withdraw ticket was created.                                                                                                                                                                                                                                                             |
| UserId      | **integer.** The user ID of the user canceling the withdrawal.                                                                                                                                                                                                                                                                                                 |
| AccountId   | **integer.** The ID of the account from which the withdraw was made.                                                                                                                                                                                                                                                                                           |
| RequestCode | <p><strong>string.</strong> The globally unique ID (GUID) that identifies the specific withdraw that is being canceled.<br><br>You can obtain the <em>RequestCode</em> for a specific withdrawal by calling <strong>GetWithdraws</strong> with the account ID and looking for the <em>withdrawCode</em> value that corresponds to this pending withdrawal.</p> |

#### Response <a href="#response" id="response"></a>

```
{
    "result": true,
    "errormsg": "Operation Failed",
    "errorcode": 101,
    "detail": "Withdraw Ticket not found for OmsId, AccountId, RequestCode"
}
```

The response indicates that the system has received the **CancelWithdraw** Request, not that the withdraw ticket has been canceled. You can check the status of a withdraw ticket by using **GetWithdrawTicket.**

| Key       | Value                                                                                                                                                                                                                                                                                                                                                                                                |
| --------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| result    | **Boolean.** A successful receipt of the withdraw ticket cancellation request returns _true;_ an unsuccessful receipt (an error condition) returns _false._                                                                                                                                                                                                                                          |
| errormsg  | <p><strong>string.</strong> A successful receipt of the withdraw ticket cancellation request returns <em>null;</em> the <em>errormsg</em> field for an unsuccessful request returns one of the following messages:<br>Not Authorized (errorcode 20)<br>Invalid Request (errorcode 100)<br>Operation Failed (errorcode 101)<br>Server Error (errorcode 102)<br>Resource Not Found (errorcode 104)</p> |
| errorcode | **integer.** A successful receipt of the withdraw ticket cancellation request returns 0. An unsuccessful receipt returns one of the _errorcodes_ shown in the _errormsg_ list.                                                                                                                                                                                                                       |
| detail    | **string.** Message text that the system may send. Usually _null._                                                                                                                                                                                                                                                                                                                                   |
