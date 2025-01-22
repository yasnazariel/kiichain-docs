# GetUserAccountInfos

**Category:** User\
**Permissions:** Operator, Trading, AccountReadOnly\
**Call Type:** Synchronous

Returns a list of account information for all accounts belonging to the specified user.

#### Request <a href="#request" id="request"></a>

```
{
  "OMSId": 0,
  "UserId": 0,
  "UserName": "",
}
```

| Key      | Value                                                                                 |
| -------- | ------------------------------------------------------------------------------------- |
| OMSId    | **integer**. The Order Management System on which the user has one ore more accounts. |
| UserId   | **integer**. The ID of the user whose accounts you want to return.                    |
| UserName | **string**. The name of the user.                                                     |

#### Response <a href="#response" id="response"></a>

> Returns a JSON list of account objects; one for each account associated with the user.

```
{
  "OMSID": 0,
  "AccountId": 0,
  "AccountName": "",
  "AccountHandle": "",
  "FirmId": "",
  "FirmName": "",
  "AccountType": {
    "Options":[
      "Asset",
      "Liability",
      "ProfitLoss"
    ] 
  },
  "FeeGroupID": 0,
  "ParentID": 0,
  "RiskType": {
    "Options": [
      "Unknown",
      "Normal",
      "NoRiskCheck",
      "NoTrading"
    ] 
  },
  "VerificationLevel": 0,
  "FeeProductType": {
    "Options": [
      "BaseProduct",
      "SingleProduct"
    ] 
  },
  "FeeProduct": 0,
  "RefererId": 0,
  "LoyaltyProductId" : 0,
  "LoyaltyEnabled" : false,
  "MarginEnabled" : false,
  "LiabilityAccountId" : 0,
  "LendingAccountId" : 0,
  "ProfitLossAccountId" : 0
}
```

| Key                   | Value                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| OMSID                 | **integer**. The ID of the Order Management System on which the account resides.                                                                                                                                                                                                                                                                                                                                                                        |
| AccountId             | **integer**. The ID of the account for which information was requested.                                                                                                                                                                                                                                                                                                                                                                                 |
| AccountName           | **string.** The name of the account.                                                                                                                                                                                                                                                                                                                                                                                                                    |
| AccountHandle         | **string**. _AccountHandle_ is a unique user-assigned name that is checked at create time by the Order Management System.                                                                                                                                                                                                                                                                                                                               |
| FirmId                | **string**. An arbitrary identifier assigned by a trading venue operator to a trading firm as part of the initial company, user, and account set up process. For example, Smith Financial Partners might have the ID SMFP.                                                                                                                                                                                                                              |
| FirmName              | **string**. A longer, non-unique version of the trading firm’s name; for example, Smith Financial Partners.                                                                                                                                                                                                                                                                                                                                             |
| AccountType           | <p><strong>string</strong>. The type of the account for which information is being returned. One of:<br>Asset<br>Liability<br>ProfitLoss<br><br>Responses for this string/value pair for Market Participants are almost exclusively <em>Asset</em>.</p>                                                                                                                                                                                                 |
| FeeGroupID            | **integer**. Defines account attributes relating to how fees are calculated and assessed. Set by trading venue operator.                                                                                                                                                                                                                                                                                                                                |
| ParentID              | **integer**. Reserved for future development.                                                                                                                                                                                                                                                                                                                                                                                                           |
| RiskType              | <p><strong>string</strong>. One of:<br>Unkown (an error condition)<br>Normal<br>NoRiskCheck<br>NoTrading<br><br>Returns <em>Normal</em> for virtually all market participants. Other types indicate account configurations assignable by the trading venue operator.</p>                                                                                                                                                                                |
| VerificationLevel     | **Integer**. Verification level ID (how much verification does this account require) defined by and set by the trading venue operator for this account.                                                                                                                                                                                                                                                                                                 |
| FeeProductType        | <p><strong>string</strong>. One of:<br>BaseProduct<br>SingleProduct<br><br>Transaction fees may be charged by a trading venue operator. This value shows whether fees for this account’s trades are charged in the product being traded (<em>BaseProduct</em>, for example BitCoin) or whether the account has a preferred fee-paying product (<em>SingleProduct</em>, for example USD) to use in all cases and regardless of product being traded.</p> |
| FeeProduct            | **integer**. The ID of the preferred fee product, if _SingleProduct_ is the value of _FeeProductType_.                                                                                                                                                                                                                                                                                                                                                  |
| RefererId             | **integer**. Captures the ID of the person who referred this account to the trading venue, usually for marketing purposes.                                                                                                                                                                                                                                                                                                                              |
| Loyalty Product Id    | **integer**. The ID of the loyalty product associated with the account.                                                                                                                                                                                                                                                                                                                                                                                 |
| Loyalty Enabled       | **boolean.** Indicates whether loyalty is enabled for the account.                                                                                                                                                                                                                                                                                                                                                                                      |
| Margin Enabled        | **boolean**. Indicates whether margin trading is enabled for the account.                                                                                                                                                                                                                                                                                                                                                                               |
| Liability Account Id  | **integer.** The ID of the liability account associated with this account.                                                                                                                                                                                                                                                                                                                                                                              |
| Lending Account Id    | **integer.**  The ID of the lending account associated with this account.                                                                                                                                                                                                                                                                                                                                                                               |
| Profit Loss AccountId | **integer.** The ID of the profit and loss account associated with this account.                                                                                                                                                                                                                                                                                                                                                                        |
