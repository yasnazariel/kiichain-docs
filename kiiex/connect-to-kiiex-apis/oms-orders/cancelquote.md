# CancelQuote

**Category:** User\
**Permissions:** Operator, Marketmaker\
**Call Type:** Synchronous

Cancels a quote that has not been executed yet.

**Note:** Quoting is not enabled for the retail end user of the AlphaPoint software. Only registered market participants or marketmakers may quote. Only a user with Operator permission can cancel quotes for another user.

#### Request <a href="#request" id="request"></a>

```
{
    "omsId": 0,
    "accountId": 0,
    "instrumentId": 0,
    "bidQuoteId": 0,
    "askQuoteId": 0
}
```

You must identify the quote to be canceled by both _BidQuoteId_ and _AskQuoteId_, which were supplied by the system when the quote was created. You can optionally identify the canceled quote using _AccountId_ and _InstrumentId_. If the call does not include _AccountId_, the call assumes the default _AccountId_ for the logged-in user; if the call does not include _InstrumentId_, the call operates on any instruments quoted by the account.

| Key          | Value                                                                                       |
| ------------ | ------------------------------------------------------------------------------------------- |
| omsId        | **integer.** The ID of the Order Management System where the quote was requested. Required. |
| accountId    | **integer.** The ID of the account that requested the quote. _Conditionally optional_.      |
| instrumentId | **long integer.** The ID of the instrument being quoted. _Conditionally optional_.          |
| bidQuoteId   | **integer.** The ID of the bid quote. _Required_.                                           |
| askQuoteId   | **integer.** The ID of the ask quote. _Required_.                                           |

#### Response <a href="#response" id="response"></a>

```
{
  "BidResult": "{
    "result": true,
    "errormsg": "",
    "errorcode": 0,
    "detail": "",
  }",
  "AskResult": "{
    "result": true,
    "errormsg": "",
    "errorcode": 0,
    "detail": "",
  }"
}
```

Returns two json objects, one for Bid and one for Ask.

The response to **CancelQuote** verifies that the call was received, not that the quote has been canceled successfully. Individual event updates to the user show quotes as they cancel. To verify that a quote has been canceled, use **GetOpenQuotes.**

| Key       | Value                                                      |
| --------- | ---------------------------------------------------------- |
| BidResult | **object.** Returns a response object for Bid (see below). |
| AskResult | **object.** Returns a response object for Ask.             |

Objects for both _BidResult_ and _AskResult_:

| Key       | Value                                                                                                                                                                                                                                                                                                                                                                                                                      |
| --------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| result    | **Boolean.** A successful receipt of the cancelation returns _true_; and unsuccessful receipt of the cancelation (an error condition) returns _false_.                                                                                                                                                                                                                                                                     |
| errormsg  | <p><strong>string.</strong> A successful receipt of the cancelation returns <em>null</em>; the <em>errormsg</em> parameter for an unsuccessful receipt returns one of the following messages:<br>Not Authorized (errorcode 20)<br>Invalid Request (errorcode 100)<br>Operation Failed (errorcode 101)<br>Server Error (errorcode 102)<br>Resource Not Found (errorcode 104)<br>Operation Not Supported (errorcode 106)</p> |
| errorcode | **integer.** A successful receipt of the cancelation returns 0. An unsuccessful receipt returns one of the _errorcodes_ shown in the _errormsg_ list.                                                                                                                                                                                                                                                                      |
| detail    | **string.** Message text that the system may send. Usually null.                                                                                                                                                                                                                                                                                                                                                           |

