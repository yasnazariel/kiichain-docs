# SendOrder

**Category:** User\
**Permissions:** Operator, Trading\
**Call Type:** Asynchronous

Creates an order.

Anyone submitting an order should also subscribe to the various market data and event feeds, or call **GeOpenOrders** or **GetOrderStatus** to monitor the status of the order. If the order is not in a state to be executed, **GetOpenOrders** will not return it.

A user with Trading permission can create an order only for those accounts and instruments with which the user is associated; a user with Operator permissions can create an order for any account and instrument.

**Note:** Call Type is asynchronous.

#### Request <a href="#request" id="request"></a>

```
 {
     "InstrumentId": 1,
     "OMSId": 1,
     "AccountId": 1,
     "TimeInForce": 1,
     "ClientOrderId": 1,
     "OrderIdOCO": 0,
     "UseDisplayQuantity": false,
     "Side": 0,
     "quantity": 1,
     "OrderType": 2,
     "PegPriceType": 3,
     "LimitPrice": 8800,
     "PostOnly" : false
 }
```

If OrderType=1 (Market), Side=0 (Buy), and LimitPrice is supplied, the Market order will execute up to the value specified

| Key                | Value                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| InstrumentId       | **integer.** The ID of the instrument being traded.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| OMSId              | **integer.** The ID of the Order Management System where the instrument is being traded.                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| AccountId          | **integer.** The ID of the account placing the order.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| TimeInForce        | <p><strong>integer.</strong> An integer that represents the period during which the new order is executable. One of:<br><strong>0</strong> Unknown (error condition)<br><strong>1</strong> GTC (good 'til canceled, the default)<br><strong>2</strong> OPG (execute as close to opening price as possible)<br><strong>3</strong> IOC (immediate or canceled)<br><strong>4</strong> FOK (fill-or-kill — fill immediately or kill immediately)<br><strong>5</strong> GTX (good 'til executed)<br><strong>6</strong> GTD (good 'til date)</p> |
| ClientOrderId      | **long integer.** A user-assigned ID for the order (like a purchase-order number assigned by a company). This ID is useful for recognizing future states related to this order. _ClientOrderId_ defaults to 0.                                                                                                                                                                                                                                                                                                                             |
| OrderIdOCO         | **long integer.** The order ID if One Cancels the Other — If this order is order A, _OrderIdOCO_ refers to the order ID of an order B (which is _not_ the order being created by this call). If order B executes, then order A created by this call is canceled. You can also set up order B to watch order A in the same way, but that may require an update to order B to make it watch this one, which could have implications for priority in the order book. See **CancelReplaceOrder** and **ModifyOrder.**                          |
| UseDisplayQuantity | **Boolean.** If you enter a Limit order with a reserve, you must set _UseDisplayQuantity_ to _true_.                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Side               | <p><strong>integer.</strong> A number representing on of the following potential sides of a trade. One of:<br><strong>0</strong> Buy<br><strong>1</strong> Sell<br><strong>2</strong> Short<br><strong>3</strong> unknown (an error condition)</p>                                                                                                                                                                                                                                                                                         |
| Quantity           | **real.** The quantity of the instrument being ordered.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| OrderType          | <p><strong>integer.</strong> A number representing the nature of the order. One of:<br><strong>0</strong> Unknown<br><strong>1</strong> Market<br><strong>2</strong> Limit<br><strong>3</strong> StopMarket<br><strong>4</strong> StopLimit<br><strong>5</strong> TrailingStopMarket<br><strong>6</strong> TrailingStopLimit<br><strong>7</strong> BlockTrade.</p>                                                                                                                                                                         |
| PegPriceType       | <p><strong>integer.</strong> When entering a stop/trailing order, set <em>PegPriceType</em> to an integer that corresponds to the type of price that pegs the stop:<br><strong>1</strong> Last<br><strong>2</strong> Bid<br><strong>3</strong> Ask<br><strong>4</strong> Midpoint</p>                                                                                                                                                                                                                                                      |
| LimitPrice         | **real.** The price at which to execute the order, if the order is a Limit order.                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| PostOnly           | **boolean.**  A boolean flag indicating whether the order should be posted only. This means the order will not execute immediately against existing orders and will instead be placed in the order book.                                                                                                                                                                                                                                                                                                                                   |

#### Response <a href="#response" id="response"></a>

```
{
  "status": "Accepted",
  "errormsg": "",
  "OrderId": 123 // Server order id
}
```

| Key      | Value                                                                                                                                                |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| status   | <p><strong>string</strong>. If the order is accepted by the system, it returns "Accepted," if not it returns "Rejected."<br>Accepted<br>Rejected</p> |
| errormsg | **string**. Any error message the server returns.                                                                                                    |
| OrderId  | **long integer**. The ID assigned to the order by the server. This allows you to track the order.                                                    |
