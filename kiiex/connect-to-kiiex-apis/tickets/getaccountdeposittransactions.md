# GetAccountDepositTransactions

**Category:** User\
**Permissions:** Trading, AccountReadOnly\
**Call Type:** Synchronous

Obtains a list of deposits for the account.

Users with Trading and AccountReadOnly permission can return deposit transactions only from an account with which they are associated.

The owner of the trading venue determines how long to retain transaction history before archiving.

**Note:** Depth in this call is a count of how many deposit transactions to report. It is not "depth of market."

#### Request <a href="#request" id="request"></a>

```
{
    "OMSId": 1,
    "AccountId": 1,
    "Depth": 200
}
```

| Key       | Value                                                                                            |
| --------- | ------------------------------------------------------------------------------------------------ |
| OMSId     | **integer.** The ID of the Order Management System on which the account transactions took place. |
| AccountId | **integer.** The ID of the account whose transactions will be returned.                          |
| Depth     | **integer.** The count of deposit transactions to be returned. Defaults to 200.                  |

#### Response <a href="#response" id="response"></a>

```
[
  {
    "transactionId": 0,
    "omsId": 0,
    "accountId": 0,
    "cr": 0.0,
    "dr": 0.0,
    "counterparty": 0,
    "transactionType": 0,
    "referenceId": 0,
    "referenceType": 0,
    "productId": 0,
    "balance": 0.0,
    "timeStamp": 0
    },
]
```

The response returns an array of transaction objects.

| Key             | Value                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| transactionId   | **Integer.** The ID of the transaction.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| omsId           | **Integer.** The ID of the Order Management System under which the requested transactions took place.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| accountId       | **Integer.** The single account under which the transactions took place.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| cr              | **real.** Credit entry for the account on the order book. Funds entering an account.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| dr              | **real.** Debit entry for the account on the order book. Funds leaving an account.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| counterparty    | **long integer.** The corresponding party in a trade.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| transactionType | <p><strong>integer.</strong> A number representing the type of transaction:<br><strong>1</strong> Fee<br><strong>2</strong> Trade<br><strong>3</strong> Other<br><strong>4</strong> Reverse<br><strong>5</strong> Hold<br><strong>6</strong> Rebate<br><strong>7</strong> MarginAcquisition<br><strong>8</strong> MarginRelinquish</p>                                                                                                                                                                                                                                                |
| referenceId     | **long integer.** The ID of the action or event that triggered this transaction.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| referenceType   | <p><strong>integer.</strong> A number representing the type of action or event that triggered this transaction. One of:<br><strong>1</strong> Trade<br><strong>2</strong> Deposit<br><strong>3</strong> Withdraw<br><strong>4</strong> Transfer<br><strong>5</strong> OrderHold<br><strong>6</strong> WithdrawHold<br><strong>7</strong> DepositHold<br><strong>8</strong> MarginHold<br><strong>9</strong> ManualHold<br><strong>10</strong> ManualEntry<br><strong>11</strong> MarginAcquisition<br><strong>12</strong> MarginRelinquish<br><strong>13</strong> MarginQuoteHold</p> |
| productId       | **integer.** The ID of the product in which the deposit was made. Use **GetProduct** to return information about a product based on its ID.                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| balance         | **real.** The balance in the account after the transaction.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| timeStamp       | **long integer.** Time at which the transaction took place, in POSIX format.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |

