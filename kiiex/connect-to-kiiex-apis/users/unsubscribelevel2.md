# UnsubscribeLevel2

**Category:** User\
**Permissions:** Operator, Trading, Level2MarketData\
**Call Type:** Synchronous

Unsubscribes the user from a Level 2 Market Data Feed subscription.

#### Request <a href="#request" id="request"></a>

```
{
    "OMSId": 1,
    "InstrumentId": 1
}
```

| Key          | Value                                                                                                              |
| ------------ | ------------------------------------------------------------------------------------------------------------------ |
| OMSId        | **integer.** The ID of the Order Management System on which the user has subscribed to a Level 2 market data feed. |
| InstrumentId | **long integer.** The ID of the instrument being tracked by the Level 2 market data feed.                          |

#### Response <a href="#response" id="response"></a>

```
{
    "result": true,
    "errormsg": null,
    "errorcode":0,
    "detail": null
}
```

| Key       | Value                                                                                                                                                                                                                                                                                                                                                                                   |
| --------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| result    | **Boolean.** A successful receipt of the unsubscribe request returns _true_; and unsuccessful receipt (an error condition) returns _false_.                                                                                                                                                                                                                                             |
| errormsg  | <p><strong>string.</strong> A successful receipt of the unsubscribe request returns <em>null</em>; the <em>errormsg</em> parameter for an unsuccessful request returns one of the following messages:<br>Not Authorized (errorcode 20)<br>Invalid Request (errorcode 100)<br>Operation Failed (errorcode 101)<br>Server Error (errorcode 102)<br>Resource Not Found (errorcode 104)</p> |
| errorcode | **integer.** A successful receipt of the unsubscribe request returns 0. An unsuccessful receipt returns one of the _errorcodes_ shown in the _errormsg_ list.                                                                                                                                                                                                                           |
| detail    | **string.** Message text that the system may send. Usually _null_.                                                                                                                                                                                                                                                                                                                      |
