# CancelOrder

**Category:** User\
**Permissions:** Operator, Trading\
**Call Type:** Synchronous

Cancels an open order that has been placed but has not yet been fully executed.

A user with Trading permission can cancel an order only for an account with which he is associated; a user with Operator permission can cancel an order for any account.

#### Request <a href="#request" id="request"></a>

```
{
  "OMSId": 0,
  "AccountId": 0,  // conditionally optional
  "ClOrderId": 0,  // conditionally optional
  "OrderId": 0,    // conditionally optional
}
```

The OMS ID and the Order ID precisely identify the order you wish to cancel. The Order ID is unique across an OMS.

If you specify the OMS ID and the Account ID, you must also specify at least the Client Order ID. The OMS is unable to identify the order using only the OMS ID and the Client Order ID, as the Client Order ID may not be unique.

| Key       | Value                                                                                                                                                             |
| --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| OMSId     | **integer.** The Order Management System on which the order exists. _Required_.                                                                                   |
| AccountId | **integer.** The ID of the account under which the order was placed. _Conditionally optional_.                                                                    |
| ClOrderId | **long integer.** A user-assigned ID for the order (like a purchase-order number assigned by a company). _ClientOrderId_ defaults to 0. _Conditionally optional._ |
| OrderId   | **long integer.** The order to be canceled. _Conditionally optional_.                                                                                             |

#### Response <a href="#response" id="response"></a>

```
{
  "result": true,
  "errormsg": "",
  "errorcode": 0,
  "detail": "",
}
```

The response to **CancelOrder** verifies that the call was received, not that the order has been canceled successfully. Individual event updates to the user show order cancellation. To verify that an order has been canceled, call **GetOrderStatus** or **GetOpenOrders.**

| Key       | Value                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| --------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| result    | **Boolean.** Returns _true_ if the call to cancel the order has been successfully received, otherwise returns _false_.                                                                                                                                                                                                                                                                                                                               |
| errormsg  | <p><strong>string.</strong> A successful receipt of a call to cancel an order returns <em>null</em>; the <em>errormsg</em> parameter for an unsuccessful call to cancel an order returns one of the following messages:<br>Not Authorized (errorcode 20)<br>Invalid Request (errorcode 100)<br>Operation Failed (errorcode 101)<br>Server Error (errorcode 102)<br>Resource Not Found (errorcode 104)<br>Operation Not Supported (errorcode 106)</p> |
| errorcode | **integer.** A successfully received call to cancel an order returns 0. An unsuccessfully received call to cancel an order returns one of the _errorcodes_ shown in the _errormsg_ list.                                                                                                                                                                                                                                                             |
| detail    | **string.** Message text that the system may send. The contents of this parameter are usually null.                                                                                                                                                                                                                                                                                                                                                  |
