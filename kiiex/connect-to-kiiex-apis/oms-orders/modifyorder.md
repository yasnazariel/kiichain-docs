# ModifyOrder

**Category:** User\
**Permissions:** Operator, Trading\
**Call Type:** Synchronous

Reduces an order’s quantity without losing priority in the order book. An order’s quantity can only be reduced. The other call that can modify an order — **CancelReplaceOrder** — resets order book priority, but you can use it to increase an order.

**Note:** **ModifyOrder** does not surrender or reset order book priority.

#### Request <a href="#request" id="request"></a>

```
{
  "OMSId": 0,
  "OrderId": 0,
  "InstrumentId": 0,
  "PreviousOrderRevision" : 0,
  "Quantity": 0 ,
  "AccountId" : 0
}
```

| Key                   | Value                                                                                                                                           |
| --------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| OMSId                 | **integer.** The ID of the Order Management System where the original order was placed.                                                         |
| OrderId               | **long integer.** The ID of the order to be modified. The ID was supplied by the server when the order was created.                             |
| InstrumentId          | **integer.** The ID of the instrument traded in the order.                                                                                      |
| PreviousOrderRevision | **integer.** The revision number of the previous order. This helps ensure that the modification is applied to the correct version of the order. |
| Quantity              | **real.** The new quantity of the order. This value can only be reduced from a previous quantity.                                               |
| AccountId             | **integer.** The ID of the account associated with the order being modified.                                                                    |

#### Response <a href="#response" id="response"></a>

```
{
  "result": false,
  "errormsg": "",
  "errorcode": 0,
  "detail": "",
}
```

The response acknowledges the successful receipt of your request to modify an order; it does not indicate that the order has been modified. To find if an order has been modified, check using **GetOpenOrders** and **GetOrderHistory.**

| Key       | Value                                                                                                                                                                                                                                                                                                                                                                            |
| --------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| result    | **Boolean.** The successful receipt of a modify order request returns _true_; otherwise, returns _false_. This is the acknowledgment of receipt of the request to modify, not a confirmation that the modification has taken place.                                                                                                                                              |
| errormsg  | <p><strong>string.</strong> A successful receipt of a modify request returns <em>null</em>; the <em>errormsg</em> parameter for an unsuccessful request returns one of the following messages:<br>Not Authorized (errorcode 20)<br>Invalid Request (errorcode 100)<br>Operation Failed (errorcode 101)<br>Server Error (errorcode 102)<br>Resource Not Found (errorcode 104)</p> |
| errorcode | **integer.** The receipt of a successful request to modify returns 0. An unsuccessful request returns one of the _errorcodes_ shown in the _errormsg_ list.                                                                                                                                                                                                                      |
| detail    | **string.** Message text that the system may send. Usually _null_.                                                                                                                                                                                                                                                                                                               |
