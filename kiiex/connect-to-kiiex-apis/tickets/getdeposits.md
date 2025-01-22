# GetDeposits

**Category:** System\
**Permissions:** Operator, Trading\
**Call Type:** Synchronous

Returns an array of deposit objects with information about the deposits of a specific account.

Users with Trading permission can get deposit information only for their own accounts; users with Operator permission can get deposit information for any account.

#### Request <a href="#request" id="request"></a>

```
{
    "OMSId": 1,
    "AccountId": 1
}
```

| Key       | Value                                                                               |
| --------- | ----------------------------------------------------------------------------------- |
| OMSId     | **integer.** The ID of the Order Management System on which the deposits were made. |
| AccountId | **integer.** The ID of the account into which the deposits were made.               |

#### Response <a href="#response" id="response"></a>

```
[
    {
        "omsId": 0,
        "depositId": 0,
        "accountId": 0,
        "subAccountId": 0,
        "productId": 0,
        "amount": 0.0
    },
]
```

The Response is an array of deposit objects.

| Key          | Value                                                                                                                                 |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------- |
| omsId        | **integer.** The ID of the Order Management System on which this deposit was made.                                                    |
| depositId    | **integer.** The ID of this deposit, assigned by the system.                                                                          |
| accountId    | **integer.** The ID of the account into which this deposit was made.                                                                  |
| subAccountId | **integer.** Not currently used; reserved for future use. Defaults to 0.                                                              |
| productId    | **integer.** The ID of the product or asset (the two are synonymous) that was deposited.                                              |
| amount       | **real.** The unit and fractional quantity of the product or asset that was deposited. For example 2.5 BitCoin or 2018.17 US Dollars. |
