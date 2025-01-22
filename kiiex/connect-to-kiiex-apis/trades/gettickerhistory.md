# GetTickerHistory

**Category:** User\
**Permissions:** Public\
**Call Type:** Synchronous

Requests a ticker history (high, low, open, close, volume, bid, ask, ID) of a specific instrument from a given date to the present. You will need to format the returned data per your requirements.

Because permission is Public, any user can retrieve the ticker history for any instrument on the OMS.

#### Request <a href="#request" id="request"></a>

```
{
    "InstrumentId": 1,
    "Interval": 60,
    "FromDate": "2018-07-18",
    "ToDate": "2018-07-19",
    "OMSId":1
}
```

| Key          | Value                                                                                                                                                             |
| ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| InstrumentId | **integer.** The ID of a specific instrument. The current Order Management System is assumed.                                                                     |
| Interval     | **integer.** The time between ticks, in seconds. For example, a value of 60 returns ticker array elements between _FromDate_ to _ToDate_ in 60-second increments. |
| FromDate     | **string.** Oldest date from which the ticker history will start, in Micrisoft Ticks format. The report moves toward _ToDate_ from this point.                    |
| ToDate       | **string.** Most recent date, at which the ticker history will end, in Microsoft Ticks format.                                                                    |
| OMSId        | **integer.** The ID of the Order Management System where the ticker history comes from.                                                                           |

#### Response <a href="#response" id="response"></a>

The response returns an array of arrays dating from the _FromDate_ value of the request to the _ToDate_. The data are returned oldest-date first. The data returned in the arrays are not labeled.

> The response is an array of arrays of comma-separated, but unlabeled, numbers. This sample shows comments applied to identify the data being returned (comments are not part of the response; the second array shows how the data actually is reported):

```
[
  [
    1501603632000, \\DateTime - UTC - Milliseconds since 1/1/1970 - POSIX format
    2700.33, \\High
    2687.01, \\Low
    2687.01, \\Open
    2687.01, \\Close
    24.86100992,  \\Volume
    0,  \\Inside Bid Price
    2870.95,  \\Inside Ask Price
    1 \\InstrumentId
  ],
  [1501604532000,2792.73,2667.95,2687.01,2700.81,242.61340767,0,2871,0],
]
```
