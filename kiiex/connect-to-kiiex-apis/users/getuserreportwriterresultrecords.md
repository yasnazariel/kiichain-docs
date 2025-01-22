# GetUserReportWriterResultRecords

**Category:** User\
**Permissions:** Operator, Trading\
**Call Type:** Synchronous

The call returns an array of user report writer results. The results are the details of when reports have been run and the status of each report run.

Users with Trading permission can request user report writer result records only for their own user IDs; users with Operator permission can request any user's report writer result records.

**Note:** "Depth" in this call is the count of records to be returned, not market depth.

#### Request <a href="#request" id="request"></a>

```
{
    "userId":0,
    "depth":50,
    "startIndex":0
}
```

| Key        | Value                                                                                                                                                                                                                                                                                                              |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| userId     | **integer.** The ID of the user whose report writer result records will be returned.                                                                                                                                                                                                                               |
| depth      | **integer.** The count of records to be returned, beginning at _startIndex_ and working backwards into the past. For example, for a _startIndex_ of 100 and a _depth_ of 50 **GetUserReportWriterResultRecords** will return records numbered between 100 and 149, inclusive. The value of _depth_ defaults to 50. |
| startIndex | **integer.** The record number at which the call starts returning records; from there, record return moves into the past. The most recent record is record 0. The value of _startIndex_ defaults to 50.                                                                                                            |

#### Response <a href="#response" id="response"></a>

```
[
    {
        "RequestingUser":1,
        "urtTicketId":"mGzjUfylGEmqgJIxu651aQ==",
        "descriptorId":"47TlpPQyTkKR4LKl9Hy1yA==",
        "resultStatus":"SuccessComplete",
        "reportExecutionStartTime":"2018-08-17T17:57:56Z",
        "reportExecutionCompleteTime":"2018-08-17T17:57:57Z",
        "reportOutputFilePathname":"",
        "reportDescriptiveHeader":"TradeActivity|onDemand|2018-08-10T04:00:00.000Z|2018-08-10T05:00:00.000Z|2018-08-17T17:57:51.852Z|2018-08-17T17:57:56.840Z|0.19634 seconds"
    },
]
```

| Key                         | Value                                                                                                                                                                  |
| --------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| RequestingUser              | **Integer**. ID of the user requesting the report writer result records.                                                                                               |
| urtTicketId                 | **string**. An alphanumeric string containing the unique report ID of the report.                                                                                      |
| descriptorId                | **string**. A GUID (globally-unique identifier) that describes the report separately from the report ticket.                                                           |
| resultStatus                | <p><strong>string</strong>. The status of each run of the reports. One of:<br>0 NotStarted<br>1 NotComplete<br>2 ErrorComplete<br>3 SuccessComplete<br>4 Cancelled</p> |
| reportExecutionStartTime    | **string.** The time that the report writer began execution, in Microsoft Ticks format.                                                                                |
| reportExecutionCompleteTime | **string.** The time that the report writer completed the report, in Microsoft Ticks format.                                                                           |
| reportOutputFilePathname    | **string.** The pathname (location) of the report output file.                                                                                                         |
| reportDescriptiveHeader     | **string**. A string describing the report.                                                                                                                            |
