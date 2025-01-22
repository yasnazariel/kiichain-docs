# GetUserAccounts

**Category:** User\
**Permissions:** Operator, Trading, AccountReadOnly\
**Call Type:** Synchronous

Returns a list of account IDs for a given user. More than one user may be associated with a given account.

#### Request <a href="#request" id="request"></a>

```
{
  "omsId": 0,
  "userId": 0,
  "userName": "",
}
```

| Key      | Value                                                                                 |
| -------- | ------------------------------------------------------------------------------------- |
| OMSId    | **integer**. The Order Management System on which the user has one ore more accounts. |
| UserId   | **integer**. The ID of the user whose accounts you want to return.                    |
| UserName | **string**. The name of the user.                                                     |

#### Response <a href="#response" id="response"></a>

The response returns list of comma-separated account IDs.

```
{
  0, // a list of account IDs
}
```
