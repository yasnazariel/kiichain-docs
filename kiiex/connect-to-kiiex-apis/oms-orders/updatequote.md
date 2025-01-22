# UpdateQuote

**Category:** User\
**Permissions:** Operator, MarketMaker\
**Call Type:** Synchronous

Updates an existing quote. Quoting is not enabled for the retail end user of the KIIEX software. Only registered market participants or market makers may quote.

**Warning** \*\*UpdateQuote\*\* resets the quote's priority in the order book.

#### Request <a href="#request" id="request"></a>

```
{
    "OMSId": 0,
    "AccountId": 0,
    "InstrumentId": 0,
    "BidQuoteId": 0,
    "Bid": 0,
    "BidQTY": 0,
    "AskQuoteId": 0,
    "Ask": 0,
    "AskQTY": 0,
}
```

| Key          | Value                                                                          |
| ------------ | ------------------------------------------------------------------------------ |
| OMSId        | **integer.** The ID of the Order Management System where the quote is located. |
| AccountId    | **integer.** The ID of the account whose quote will be updated.                |
| InstrumentId | **long integer.** The ID of the instrument whose quote is being updated.       |
| BidQuoteId   | **integer.** The ID of the original bid quote being updated.                   |
| Bid          | **real.** The new amount of the bid quote.                                     |
| BidQTY       | **real.** The new quantity of the bid quote.                                   |
| AskQuoteId   | **integer.** The ID of the original ask quote being updated.                   |
| Ask          | **real.** The new amount of the ask quote.                                     |
| AskQTY       | **real.** The new quantity of the ask quote.                                   |

#### Response <a href="#response" id="response"></a>

```
{
  "BidResult": {
    "result": true,
    "errormsg": "",
    "errorcode": 0,
    "detail": "",
  },
  "AskResult": {
    "result": true,
    "errormsg": "",
    "errorcode": 0,
    "detail": "",
  }
}
```

| Key       | Value                                                      |
| --------- | ---------------------------------------------------------- |
| BidResult | **object.** Returns a response object for Bid (see below). |
| AskResult | **object.** Returns a response object for Ask.             |

Objects for both _BidResult_ and _AskResult_:

| Key       | Value                                                                                                                                                                                                                                                                                                                                                                                                                 |
| --------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| result    | **Boolean.** A successful receipt of the update returns _true_; and unsuccessful receipt of the update (an error condition) returns _false_.                                                                                                                                                                                                                                                                          |
| errormsg  | <p><strong>string.</strong> A successful receipt of the update returns <em>null</em>; the <em>errormsg</em> parameter for an unsuccessful receipt returns one of the following messages:<br>Not Authorized (errorcode 20)<br>Invalid Request (errorcode 100)<br>Operation Failed (errorcode 101)<br>Server Error (errorcode 102)<br>Resource Not Found (errorcode 104)<br>Operation Not Supported (errorcode 106)</p> |
| errorcode | **integer.** A successful receipt of the update returns 0. An unsuccessful receipt returns one of the _errorcodes_ shown in the _errormsg_ list.                                                                                                                                                                                                                                                                      |
| detail    | **string.** Message text that the system may send. Usually null.                                                                                                                                                                                                                                                                                                                                                      |
