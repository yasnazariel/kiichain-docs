# GetTreasuryProductsForAccount

**Category:** User\
**Permissions:** Operator, Trading, Withdraw, Deposit\
**Call Type:** Synchronous

Returns a list of product symbols (BTC, USD, etc.) upon which the account named by AccountId is allowed to execute treasury operations.

Users with Trading, Withdraw, and Deposit permission must be associated with the account named by AccountId. Users with Operator permission can request the list of treasury products for any account.

#### Request <a href="#request" id="request"></a>

```
{
    "AccountId": 1,
    "OMSId": 1
}
```

| Key       | Value                                                                                  |
| --------- | -------------------------------------------------------------------------------------- |
| AccountId | **integer.** The ID of the account whose permitted treasury products will be returned. |
| OMSId     | **integer.** The ID of the Order Management System where the account operates.         |

#### Response <a href="#response" id="response"></a>

> An array of code symbol lists.

```
[ { "LTC", "BTC", "USD" }, ]
```

The response returns an array of code symbol lists.

