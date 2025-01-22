# CreateQuote

**Category:** User\
**Permissions:** Operator, MarketMaker\
**Call Type:** Synchronous

**TK** call and response may change

Creates a quote. A quote expresses a willingness to buy or sell at a given price. Both a quote and an order will execute. Only a user with Operator or MarketMaker permission can create a quote.

**Note:** Quoting is not enabled for the retail end user of AlphaPoint software. Only registered market participants or market makers may quote.

#### Request <a href="#request" id="request"></a>

```
{
  "OMSId": 0,
  "AccountId": 0,
  "InstrumentId": 0,
  "Bid": 0,
  "BidQty": 0,
  "Ask": 0,
  "AskQty": 0,
}
```

| Key          | Value                                                                                                                                                                                   |
| ------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| OMSId        | **integer.** The ID of the Order Management System on which the quote is being created. _Required_.                                                                                     |
| AccountId    | **integer.** The ID of the account in which the quote is being created. If the call provides no AccountId, the system assumes the default account ID for the logged-in user on the OMS. |
| InstrumentId | **long integer.** The ID of the instrument being quoted. _Required_.                                                                                                                    |
| Bid          | **real.** The bid price. _Required_.                                                                                                                                                    |
| BidQty       | **real.** The quantity of the bid. _Required_.                                                                                                                                          |
| Ask          | **real.** The ask price. _Required_.                                                                                                                                                    |
| AskQty       | **real.** The quantity of the ask. _Required_.                                                                                                                                          |

#### Response <a href="#response" id="response"></a>

```
{
  "bidQouteId" : 0,
  "BidResult": {
    "result": true,
    "errormsg": "",
    "errorcode": 0,
    "detail": "",
  },
  "askQouteId" : 0,
  "AskResult": {
    "result": true,
    "errormsg": "",
    "errorcode": 0,
    "detail": "",
  }
}
```

| Key        | Value                                                      |
| ---------- | ---------------------------------------------------------- |
| bidQouteId | **integer.** Returns the bid qoute Id.                     |
| BidResult  | **object.** Returns a response object for Bid (see below). |
| askQouteId | **integer.** Returns ask qoute Id.                         |
| AskResult  | **object.** Returns a response object for Ask.             |

Objects for both _BidResult_ and _AskResult_:

| Key       | Value                                                                                                                                                                                                                                                                                                                                                                                                                      |
| --------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| result    | **Boolean.** A successful receipt of the cancelation returns _true_; and unsuccessful receipt of the cancelation (an error condition) returns _false_.                                                                                                                                                                                                                                                                     |
| errormsg  | <p><strong>string.</strong> A successful receipt of the cancelation returns <em>null</em>; the <em>errormsg</em> parameter for an unsuccessful receipt returns one of the following messages:<br>Not Authorized (errorcode 20)<br>Invalid Request (errorcode 100)<br>Operation Failed (errorcode 101)<br>Server Error (errorcode 102)<br>Resource Not Found (errorcode 104)<br>Operation Not Supported (errorcode 106)</p> |
| errorcode | **integer.** A successful receipt of the cancelation returns 0. An unsuccessful receipt returns one of the _errorcodes_ shown in the _errormsg_ list.                                                                                                                                                                                                                                                                      |
| detail    | **string.** Message text that the system may send. Usually null.                                                                                                                                                                                                                                                                                                                                                           |

