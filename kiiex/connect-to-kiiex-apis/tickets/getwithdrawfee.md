# GetWithdrawFee

**Category:** User\
**Permissions:** Operator, Trading, Withdraw\
**Call Type:** Synchronous

Gets an estimate of a fee for a withdrawal. The Products function of the KIIEX Admin can set withdraw fees OMS-wide. You can also set a withdraw fee programmatically using **SetOMSFee,** but **SetOMSFee** is a System (not User) call with permission reserved to an exchange operator. Exchange-wide withdrawal fees cannot be overridden.

A user with Trading or Withdraw permissions can obtain withdrawal fee estimates only for products and accounts with which the user is associated; a user with Operator permission can obtain withdrawal fee estimates for any product or account.

#### Request <a href="#request" id="request"></a>

```
{
    "OMSId": 1,
    "AccountId": 1,
    "ProductId": 1,
    "Amount": 1,
    "AccountProviderId" : 1
}
```

| Key               | Value                                                                                    |
| ----------------- | ---------------------------------------------------------------------------------------- |
| OMSId             | **integer.** The ID of the Order Management System trading the product.                  |
| AccountId         | **integer.** The ID of the account making the withdrawal.                                |
| ProductId         | **integer.** The ID of the product intended to be withdrawn. Fees may vary with product. |
| Amount            | **real.** The amount of product intended to be withdrawn.                                |
| AccountProviderId | **real.** The Id of the Account provider                                                 |

#### Response <a href="#response" id="response"></a>

```
{
    "FeeAmount":1.06,
    "TicketAmount" : 10.24
}
```

| Key          | Value                                                                   |
| ------------ | ----------------------------------------------------------------------- |
| FeeAmount    | **real.** The estimated amount of the fee for the indicated withdrawal. |
| TicketAmount | **real.** The estimated amount to withdraw                              |

