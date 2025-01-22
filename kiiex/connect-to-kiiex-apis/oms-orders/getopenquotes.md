# GetOpenQuotes

**Category:** User\
**Permissions:** Operator, MarketMaker\
**Call Type:** Synchronous

Returns the current bid and ask quotes for a given instrument ID and account ID.

#### Request <a href="#request" id="request"></a>

```
{
  "omsId": 0,
  "accountId": 0,
  "instrumentId": 0,
}
```

| Key          | Value                                                                                                      |
| ------------ | ---------------------------------------------------------------------------------------------------------- |
| OMSId        | **integer**. The ID of the Order Management System where the instrument is traded whose quote may be open. |
| AccountId    | **integer**. The ID of the account whose open quotes will be returned.                                     |
| InstrumentId | **integer**. The ID of the instrument being quoted.                                                        |

#### Response <a href="#response" id="response"></a>

```
{
    "bid": {
        "omsId": 0,
        "side": 0,
        "orderId": 0,
        "price": 0.0,
        "quantity": 0.0,
        "displayQuantity": 0.0,
        "instrument": 0,
        "account": 0,
        "orderType": 0,
        "clientOrderId": 0,
        "orderState": 0
    },
    "ask": {
        "omsId": 0,
        "side": 0,
        "orderId": 0,
        "price": 0.0,
        "quantity": 0.0,
        "displayQuantity": 0.0,
        "instrument": 0,
        "account": 0,
        "orderType": 0,
        "clientOrderId": 0,
        "orderState": 0
    }
}
```

Returns a JSON object comprising a bid and an ask object. Both object comprise the same key-value pairs.

| Key | Value                  |
| --- | ---------------------- |
| bid | Bid object (see below) |
| ask | Ask object (see below) |

Bid and Ask objects differ only in the values for the keys.

| Key             | Value                                                                                                                                                                                                                                                                                                                                                                              |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| omsId           | **integer.** The ID of the Order Management System containing the open quotes.                                                                                                                                                                                                                                                                                                     |
| side            | <p><strong>integer.</strong> One of:<br><strong>0</strong> Buy<br><strong>1</strong> Sell<br><strong>2</strong> Short<br><strong>3</strong> Unknown (error condition)</p>                                                                                                                                                                                                          |
| orderId         | **long integer.** The ID of this quote. Quotes and orders are both executable, but only Operators and MarketMakers may quote.                                                                                                                                                                                                                                                      |
| price           | **real.** Price of the Bid/Ask quote.                                                                                                                                                                                                                                                                                                                                              |
| quantity        | **real.** Quantity of the Bid/Ask quote.                                                                                                                                                                                                                                                                                                                                           |
| displayQuantity | **real.** The quantity available to buy or sell that is publicly displayed to the market. To display a _DisplayQuantity_ value, an order must be a Limit order with a reserve.                                                                                                                                                                                                     |
| instrument      | **integer.** The ID of the instrument being quoted.                                                                                                                                                                                                                                                                                                                                |
| account         | **integer.** The ID of the account quoting the instrument.                                                                                                                                                                                                                                                                                                                         |
| orderType       | <p><strong>integer.</strong> A number describing the type of order (or in this case, quote). One of:<br><strong>0</strong> Unknown<br><strong>1</strong> Market<br><strong>2</strong> Limit<br><strong>3</strong> StopMarket<br><strong>4</strong> StopLimit<br><strong>5</strong> TrailingStopMarket<br><strong>6</strong> TrailingStopLimit<br><strong>7</strong> BlockTrade</p> |
| ClientOrderId   | **long integer.** A user-assigned ID for the quote (like a purchase-order number assigned by a company). _ClientOrderId_ defaults to 0.                                                                                                                                                                                                                                            |
| orderState      | <p><strong>integer.</strong> A number describing the current state of the order. One of:<br><strong>0</strong> Unknown<br><strong>1</strong> Working<br><strong>2</strong> Rejected<br><strong>3</strong> Canceled<br><strong>4</strong> Expired<br><strong>5</strong> FullyExecuted<br><br>An open quote will probably have an <em>OrderState</em> of Working.</p>                |
