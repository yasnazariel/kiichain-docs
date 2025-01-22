# GetAccountTrades

**Category:** User\
**Permissions:** Operator, Trading, AccountReadOnly\
**Call Type:** Synchronous

Requests the details on up to 200 past trade executions for a single specific account and Order Management System, starting at index _i_, where _i_ is an integer identifying a specific execution in reverse order; that is, the most recent execution has an index of 0, and increments by one as trade executions recede into the past.

Users with Trading or AccountReadOnly permission may access trade information only for accounts with which they are associated; users with Operator permission may access trade information for any account.

The operator of the trading venue determines how long to retain an accessible trading history before archiving.

#### Request <a href="#request" id="request"></a>

```
{
    "OMSId": 0,
    "accountId" : 0,
    "executionId" : 0,
    "tradeId" : 0,
    "orderId" ; 0, 
    "userId": 0,
    "startTimestamp" : 0,
    "endTimestamp" 0,
    "depth" : 100,
    "StartIndex":0
}
```

| Key             | Value                                                                                                                                                    |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| OMSId           | **integer.** The ID of the Order Management System to which the user belongs. A user will belong to only one OMS.                                        |
| AccountId       | **integer.** The ID of the account.                                                                                                                      |
| execution Id    | **integer.** The specific execution ID to retrieve trades for. A value of `0` typically means that trades for all executions should be retrieved.        |
| trade Id        | **integer.** The specific trade ID to retrieve details for. A value of `0` typically means that all trades should be retrieved, not just a specific one. |
| order Id        | **integer.** The specific order ID to retrieve trades for. A value of `0` typically means that trades for all orders should be retrieved.                |
| user Id         | **integer.** The ID of the user who owns the account for which trade history is being retrieved.                                                         |
| start Timestamp | **timestamp.** The starting timestamp (in seconds since the epoch) for the period over which trades should be retrieved.                                 |
| end Timestamp   | **timestamp.** The ending timestamp (in seconds since the epoch) for the period over which trades should be retrieved.                                   |
| depth           | **integer.** The maximum number of trade records to retrieve. This limits the number of trades returned by the request.                                  |
| execution Id    | **integer.** The specific execution ID to retrieve trades for. A value of `0` typically means that trades for all executions should be retrieved.        |
| StartIndex      | **integer.** The starting index into the history of trades, beginning from 0 (the most recent trade).                                                    |
|                 |                                                                                                                                                          |

#### Response <a href="#response" id="response"></a>

```
[
    {
        "OMSId": 0,
        "ExecutionId": 0,
        "TradeId": 0,
        "OrderId": 0,
        "AccountId": 0,
        "AccountName": "",
        "SubAccountId": 0,
        "ClientOrderId": 0,
        "InstrumentId": 0,
        "Side": "Buy",
        "OrderType": "Limit"
        "Quantity": 0.0,
        "RemainingQuantity": 0.0,
        "Price": 0.0,
        "Value": 0.0,
        "CounterParty": "",
        "OrderTradeRevision": 0,
        "Direction": 0,
        "IsBlockTrade": false,
        "Fee": 0.0,
        "FeeProductId": 0,
        "OrderOriginator": 0,
        "UserName": "",
        "TradeTimeMS": 0,
        "MakerTaker": "Maker",
        "AdapterTradeId": 0,
        "InsideBid": 0,
        "InsideBidSize": 0,
        "InsideAsk": 0,
        "InsideAskSize": 0,
        "IsQuote": 0,
        "TradeTime": 0
    },
]
```

The response is an array of objects, each element of which represents the account’s side of a trade (either buy or sell).

| Key                | Value                                                                                                                                                                                                                |
| ------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| OMSId              | **integer.** The ID of the Order Management System to which the account belongs.                                                                                                                                     |
| ExecutionId        | **integer.** The ID of this account's side of the trade. Every trade has two sides.                                                                                                                                  |
| TradeId            | **integer.** The ID of the overall trade.                                                                                                                                                                            |
| OrderId            | **long integer.** The ID of the order causing the trade (buy or sell).                                                                                                                                               |
| AccountId          | **integer.** The ID of the account that made the trade (buy or sell).                                                                                                                                                |
| AccountName        | **string.** The Name of the account that made the trade (buy or sell).                                                                                                                                               |
| SubAccountId       | **integer.** Not currently used; reserved for future use. Defaults to 0.                                                                                                                                             |
| ClientOrderId      | **long integer.** An ID supplied by the client to identify the order (like a purchase order number). The _clientOrderId_ defaults to 0 if not supplied.                                                              |
| InstrumentId       | **integer.** The ID of the instrument being traded. An instrument comprises two products, for example Dollars and BitCoin.                                                                                           |
| Side               | <p><strong>string.</strong> One of the following potential sides of a trade:<br><strong>0</strong> Buy<br><strong>1</strong> Sell<br><strong>2</strong> Short<br><strong>3</strong> Unknown (an error condition)</p> |
| OrderType          | <p><strong>string.</strong> One of the following potential sides of a trade:<br>Market<br>Limit<br>BlockTrade<br>StopMarket<br>StopLimit<br>TrailingStopLimit<br>StopMarket<br>TrailingStopMarket</p>                |
| Quantity           | **real.** The unit quantity of this side of the trade.                                                                                                                                                               |
| RemainingQuantity  | **real.** The number of units remaining to be traded by the order after this execution. This number is not revealed to the other party in the trade. This value is also known as "leave size" or "leave quantity."   |
| Price              | **real.** The unit price at which the instrument traded.                                                                                                                                                             |
| Value              | <p><strong>real.</strong> The total value of the deal. The system calculates this as:<br>unit price X quantity executed.</p>                                                                                         |
| CounterParty       | **string.** The ID of the other party in a block trade. Usually, IDs are stated as integers; this value is an integer written as a string.                                                                           |
| OrderTradeRevision | **integer.** The revision number of this trade; usually 1.                                                                                                                                                           |
| Direction          | <p><strong>integer.</strong> The effect of the trade on the instrument's market price. One of:<br><strong>0</strong> No change<br><strong>1</strong> Uptick<br><strong>2</strong> DownTick</p>                       |
| IsBlockTrade       | **Boolean.** A value of _true_ means that this trade was a block trade; a value of _false_ that it was not a block trade.                                                                                            |
| Fee                | **real.** Any fee levied against the trade by the Exchange.                                                                                                                                                          |
| FeeProductId       | **integer.** The ID of the product in which the fee was levied.                                                                                                                                                      |
| OrderOriginator    | **integer.** The ID of the user who initiated the trade.                                                                                                                                                             |
| UserName           | **integer.** The UserName of the user who initiated the trade.                                                                                                                                                       |
| TradeTimeMS        | **long integer.** The date and time that the trade took place, in milliseconds and POSIX format. All dates and times are UTC.                                                                                        |
| MakerTaker         | <p><strong>string.</strong> One of the following potential liquidity provider of a trade:<br>Maker<br>Taker<br></p>                                                                                                  |
| AdapterTradeId     | **integer.** The ID of the adapter of the overall trade.                                                                                                                                                             |
| InsideBid          | **real.** The best (highest) price level of the buy side of the book at the time of the trade.                                                                                                                       |
| InsideBidSize      | **real.** The quantity of the best (highest) price level of the buy side of the book at the time of the trade.                                                                                                       |
| InsideAsk          | **real.** The best (lowest) price level of the sell side of the book at the time of the trade.                                                                                                                       |
| InsideAskSize      | **real.** The quantity of the best (lowest) price level of the sell side of the book at the time of the trade.                                                                                                       |
| TradeTime          | **long integer.** The date and time that the trade took place, in C# Ticks. All dates and times are UTC.                                                                                                             |
