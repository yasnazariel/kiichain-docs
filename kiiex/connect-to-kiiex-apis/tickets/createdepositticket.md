# CreateDepositTicket

**Category:** System\
**Permissions:** Operator, Trading\
**Call Type:** Synchronous

**CreateDepositTicket** records a deposit ticket for deposits of fiat money (non-crypto national currencies, for example). Crypto-currencies, such as BitCoin or Monero are handled by a different deposit mechanism described in **GetDepositInfo.**

The ticketing mechanism of the Order Management System tracks deposits and withdrawals, interacting with the Asset Manager.

#### Request <a href="#request" id="request"></a>

```
{
    "assetManagerId": 0,
    "accountId": 0,
    "assetId": 0,
    "assetName": null,
    "amount": 0.0,
    "omsId": 0,
    "requestCode": null,
    "requestIP": null,
    "requestUserName": null,
    "operatorId": 0,
    "Status": 0,
    "feeAmt": 0.0,
    "updatedByUser": 0,
    "updatedByUserName": null,
    "ticketNumber": 0,
    "depositInfo": "",
    "createdTimestamp": "0001-01-01T00:00:00",
    "lastUpdateTimeStamp": "0001-01-01T00:00:00",
    "comments": null,
    "attachments": null
}
```

| Key                 | Value                                                                                                                                                                                                                                                          |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| assetManagerId      | **integer.** The ID of the system's asset manager module, usually 1.                                                                                                                                                                                           |
| accountId           | **integer.** The account receiving the deposit.                                                                                                                                                                                                                |
| assetId             | **integer.** The ID of the asset being deposited. An asset is functionally the same as a product; you can obtain a list of products/assets available on the Exchange by using **GetProducts.**                                                                 |
| assetName           | **string.** The short name of the asset being deposited. For example, USD (US Dollars) or BTC (BitCoin).                                                                                                                                                       |
| amount              | **real.** The quantity of the asset being deposited. This is not the monetary value of the asset. For example, 2.5 BitCoins is 2.5.                                                                                                                            |
| omsId               | **integer.** The ID of the Order Management System where the deposit is being made, usually 1.                                                                                                                                                                 |
| requestCode         | **string.** A _requestCode_ is a globally unique ID assigned by the system. Leave the value for this string null when issuing the **CreateDepositTicket** call; the Response returns the value for the _requestCode,_ which you may need for other calls.      |
| requestIp           | **string.** The IP address from which the calling user makes the deposit ticket request.                                                                                                                                                                       |
| requestUserName     | **string.** The user name of the user making the deposit ticket request, for example, jsmith.                                                                                                                                                                  |
| operatorId          | **integer.** The ID of the trading venue operator.                                                                                                                                                                                                             |
| status              | **integer.** The current status of the deposit, stated as a number. A new deposit will always have a status of 0.                                                                                                                                              |
| feeAmt              | **real.** The amount of any fee for the deposit.                                                                                                                                                                                                               |
| updatedByUser       | **integer.** If the deposit ticket has been updated, this field contains the user ID of the user who updated the ticket. Because **CreateDepositTicket** creates the ticket, it is unlikely to have been updated yet; this value should be 0.                  |
| updatedByUserName   | **string.** If the deposit ticket has been updated, this field contains the name of the user who updated the ticket. Because **CreateDepositTicket** creates the ticket, it is unlikely to have been updated yet; this value should be an empty string (null). |
| ticketNumber        | **long integer.** A number assigned by the calling user to identify this deposit ticket, much as a purchase order identifies an order.                                                                                                                         |
| depositInfo         | **object.** Leave this string as empty: " ".                                                                                                                                                                                                                   |
| createdTimeStamp    | **string.** The time and date stamp for when the deposit ticket was created, in Microsoft Ticks format. All time and date stamps are given as UTC.                                                                                                             |
| lastUpdateTimeStamp | **string.** The time and date stamp for the last update to the deposit ticket after it was created. Because **CreateDepositTicket** creates the ticket, it is unlikely that it has been updated, and this string should be empty.                              |
| comments            | **string.** Any comments appended to the deposit ticket.                                                                                                                                                                                                       |
| attachments         | **string.** Any attachments appended to the deposit ticket.                                                                                                                                                                                                    |
|                     |                                                                                                                                                                                                                                                                |

#### Response <a href="#response" id="response"></a>

```
{
    "success": true,
    "requestcode": "866f21fe-3461-41d1-91aa-5689bc38503f",
}
```

The successful response to **CreateDepositTicket** is a Boolean _true_ value and a request code to allow tracking the ticket. To view and confirm ticket contents, use the call **GetDepositTicket.**

| String      | Value                                                                                                         |
| ----------- | ------------------------------------------------------------------------------------------------------------- |
| success     | **Boolean.** Returns true if the system has created the deposit ticket successfully; otherwise returns false. |
| requestcode | **string.** A globally-unique ID (GUID) that identifies this specific deposit ticket.                         |

An unsuccessful response to **CreateDepositTicket** is a standard response object that includes an error code and error message, as explained in "Standard response objects and common error codes" in **Background Information.**
