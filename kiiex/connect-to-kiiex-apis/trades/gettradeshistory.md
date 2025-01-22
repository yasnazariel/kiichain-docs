# GetTradesHistory

**Category:** User\
**Permissions:** Operator, Trading, Manual trader\
**Call Type:** Synchronous

Retrieves a list of trades for a specified account, order ID, user, instrument, or starting and ending time stamp. The returned list begins at start index _i,_ where _i_ is an integer identifying a specific trade in reverse order; that is, the most recent trade has an index of 0. “Depth” is the count of trades to report backwards from _StartIndex_.

Users with Trading permission can retrieve trade history for accounts with which they are associated; users with Operator permission can retrieve trade history for any account.

**Caution**: You must coordinate \*StartIndex\*, \*Depth\*, \*StartTimeStamp\*, and \*EndTimeStamp\* to retrieve the historical information you need. As the diagram shows, it is possible to specify values (for example, \*EndTimeStamp\* and \*Depth\*) that can exclude information you may want (the red areas).

**Note**: In this call, “Depth” refers not to the depth of the order book, but to the count of trades to report. The owner of the trading venue determines how long to retain order history before archiving.

#### Request <a href="#request" id="request"></a>

> All values in the request other than omsId are optional.

```
{
    "omsId": 0,
    "accountId": 0,
    "instrumentId": 0,
    "tradeId": 0,
    "orderId": 0,
    "userId": 0,
    "startTimestamp": 0,
    "endTimestamp": 0,
    "depth": 100,
    "startIndex": 0,
    "executionId": 0
}
```

| Key            | Value                                                                                                                                                                                                                                                                              |
| -------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| omsId          | **Integer.** The ID of the Order Management System on which the trades took place. If no other values are specified, **GetTradesHistory** returns the trades associated with the default account for the logged-in user on this Order Management System. _Required key and value._ |
| accountId      | **Integer.** The account ID that made the trades. If no account ID is supplied, the system assumes the default account for the logged-in user making the call.                                                                                                                     |
| instrumentId   | **long integer.** The ID of the instrument whose trade history is reported. If no instrument ID is included, the system returns trades for all instruments associated with the account ID and OMS.                                                                                 |
| tradeId        | **integer.** The ID of a specific trade. If you specify _TradeId_, **GetTradesHistory** can return all states for a single trade.                                                                                                                                                  |
| orderId        | **integer.** The ID of the order resulting in the trade. If specified, the call returns all trades associated with the order.                                                                                                                                                      |
| userId         | **integer.** The ID of the logged-in user. If not specified, the call returns trades associated with the users belonging to the default account for the logged-in user of this OMS.                                                                                                |
| startTimeStamp | **long integer.** The historical date and time at which to begin the trade report, in POSIX format. If not specified, reverts to the start date of this account on the trading venue.                                                                                              |
| endTimeStamp   | **long integer.** Date at which to end the trade report, in POSIX format.                                                                                                                                                                                                          |
| depth          | **integer.** In this case, the count of trades to return, counting from the _StartIndex_. If _Depth_ is not specified, returns all trades between _BeginTimeStamp_ and _EndTimeStamp_, beginning at _StartIndex_.                                                                  |
| startIndex     | **integer.** The starting index into the history of trades, from 0 (the most recent trade) and moving backwards in time. If not specified, defaults to 0.                                                                                                                          |
| executionId    | **integer.** The ID of the individual buy or sell execution. If not specified, returns all.                                                                                                                                                                                        |

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
