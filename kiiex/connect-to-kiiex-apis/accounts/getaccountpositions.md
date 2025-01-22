# GetAccountPositions

**Category:** User\
**Permissions:** Operator, Trading, AccountReadOnly, Manual Trader\
**Call Type:** Synchronous

Retrieves a list of positions (balances) for a specific user account running under a specific Order Management System. The trading day runs from UTC Midnight to UTC Midnight.

Users with Trading or AccountReadOnly permission must specify an account ID with which they're associated on the Order Management System. Users with Operator permission can specify other accounts.

#### Request <a href="#request" id="request"></a>

```
{
  "AccountId":4,
  "OMSId": 1,
  "IncludePending" : false
}
```

| Key             | Value                                                                                                                        |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| AccountId       | **integer.** The ID of the authenticated user’s account on the Order Management System for which positions will be returned. |
| OMSId           | **integer.** The ID of the Order Management System to which the user belongs. A user will belong only to one OMS.            |
| Include Pending | **boolean** . To know if will include pending positions                                                                      |

#### Response <a href="#response" id="response"></a>

```
[
    {
        "omsId":1,
        "accountId":4,
        "productSymbol":"BTC",
        "productId":1,
        "amount":0.0,
        "hold":0.0,
        "pendingDeposits":0.0,
        "pendingWithdraws":0.0,
        "totalDayDeposits":0.0,
        "totalMonthDeposits":0.0,
        "totalYearDeposits":0.0,
        "totalYearDepositNotional":0.0,
        "totalDayWithdraws":0.0,
        "totalMonthWithdraws":0.0,
        "totalYearWithdraws":0.0,
        "totalYearWithdrawNotional":0.0,
        "notionalHoldAmount": 0.0,
        "notionalRate": 0.0,
        "totalDayDepositNotional": 0.0,
        "totalMonthDepositNotional": 0.0,
        "totalDayWithdrawNotional": 0.0,
        "totalMonthWithdrawNotional": 0.0
    },
    {
        "omsId":1,
        "accountId":4,
        "productSymbol":"USD",
        "productId":2,
        "amount":0.0,
        "hold":0.0,
        "pendingDeposits":0.0,
        "pendingWithdraws":0.0,
        "totalDayDeposits":0.0,
        "totalMonthDeposits":0.0,
        "totalYearDeposits":0.0,
        "totalYearDepositNotional":0.0,
        "totalDayWithdraws":0.0,
        "totalMonthWithdraws":0.0,
        "totalYearWithdraws":0.0,
        "totalYearWithdrawNotional":0.0,
        "notionalHoldAmount": 0.0,
        "notionalRate": 0.0,
        "totalDayDepositNotional": 0.0,
        "totalMonthDepositNotional": 0.0,
        "totalDayWithdrawNotional": 0.0,
        "totalMonthWithdrawNotional": 0.0
    }
]
```

The response returns an array of one or more positions for the account. This example response has returned two positions.

| Key                       | Value                                                                                                                                                                                                                                                             |
| ------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| omsId                     | **Integer.** The ID of the Order Management System (OMS) to which the user belongs. A user will only ever belong to one Order Management System. Note the change in capitalization from the request.                                                              |
| accountId                 | **integer.** Returns the ID of the user’s account to which the positions belong. Note the change in capitalization from the request.                                                                                                                              |
| productSymbol             | <p><strong>string.</strong> The symbol of the product on this account’s side of the trade. For example:<br>BTC — BitCoin<br>USD — US Dollar<br>NZD — New Zealand Dollar<br><br>Many other values are possible depending on the nature of the trading venue.</p>   |
| productId                 | **integer.** The ID of the product being traded. The system assigns product IDs as they are entered into the system. Use **GetProduct** to return information about the product by its ID.                                                                        |
| amount                    | **real.** Unit amount of the product; for example, 10 or 138.5.                                                                                                                                                                                                   |
| hold                      | **real.** Amount of currency held and not available for trade. A pending trade of 100 units at $1 each will reduce the amount in the account available for trading by $100 and produce a $100 hold. Amounts on hold cannot be withdrawn while a trade is pending. |
| pendingDeposits           | **real.** Deposits accepted but not yet cleared for trade.                                                                                                                                                                                                        |
| pendingWithdraws          | **real.** Withdrawals acknowledged but not yet cleared from the account. Amounts in _PendingWithdraws_ are not available for trade.                                                                                                                               |
| totalDayDeposits          | **real.** Total deposits on today’s date. The trading day runs between UTC Midnight and UTC Midnight.                                                                                                                                                             |
| totalMonthDeposits        | **real.** Total deposits for the month as of today's date.                                                                                                                                                                                                        |
| totalYearDeposits         | **real.** Total deposits for the year as of today's date.                                                                                                                                                                                                         |
| totalYearDepositNotional  | <p><strong>real.</strong> Yearly amount for deposit of crypto-currencies. It is usually calculated as<br>value = (Amount * Bid/Ask Price). 10 BitCoin each at $6700 equals $67000.</p>                                                                            |
| totalDayWithdraws         | **real.** Total withdrawals on today’s date. The trading day runs between UTC Midnight and UTC Midnight.                                                                                                                                                          |
| totalMonthWithdraws       | **real.** Total withdrawals during this month to date. The trading day runs between UTC Midnight and UTC Midnight — likewise a month begins at UTC Midnight on the first day of the month.                                                                        |
| totalYearWithdraws        | **real.** Total withdrawals during the current year to date.                                                                                                                                                                                                      |
| totalYearWithdrawNotional | <p><strong>real.</strong> Yearly withdrawals for crypto-currencies. It is usually calculated as<br>value = (Amount * Bid/Ask Price). 10 BitCoin each at $6700 equals $67000.</p>                                                                                  |
|                           |                                                                                                                                                                                                                                                                   |
