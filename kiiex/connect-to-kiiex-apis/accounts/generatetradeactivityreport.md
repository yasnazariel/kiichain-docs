# GenerateTradeActivityReport

**Category:** User\
**Permissions:** Operator, Trading\
**Call Type:** Synchronous

Creates an immediate report on historical trade activity on a specific Order Management System for a list of accounts during a specified time interval.

A user with Trading permission can only generate reports for accounts with which he is associated; a user with Operator permission can generate reports for accounts associated with others.

The Trade Activity Report is delivered as a comma-separated (CSV) file. For specific CSV formatting information, see the APEX Extract CSV Data Dictionary, available from AlphaPoint.

#### Request <a href="#request" id="request"></a>

```
{
    "accountIdList": [
        0 // one or more Account IDs
    ],
    "omsId": 0,
    "startTime": "0001-01-01T05:00:00Z",
    "endTime": "0001-01-01T05:00:00Z",
}
```

| Key           | Value                                                                                                                                                                                                        |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| accountIdList | **integer array.** A comma-delimited array of one ore more account IDs, each valid on a single Order Management System for the authenticated user. The account user may not be the only user of the account. |
| omsId         | **integer.** The ID of the Order Management System on which the array of account IDs exist.                                                                                                                  |
| startTime     | **string.** _startTime_ identifies the time and date for the historic beginning of the trade activity report.                                                                                                |
| endTime       | **string.** _endTime_ identifies the time and date for the historic end of the trade activity report.                                                                                                        |

#### Response <a href="#response" id="response"></a>

```
{
  "RequestingUser":1,
  "OMSId":1,
  "reportFlavor": {
         "Options": [
            "TradeActivity",
            "Transaction",
            "Treasury"
        ] 
    },
  "createTime":"2018-08-17T15:34:20Z",
  "initialRunTime":"2018-08-17T15:34:20Z",
  "intervalStartTime":"2019-04-10T04:00:00Z",
  "intervalEndTime":"2020-04-10T04:00:00Z",
  "RequestStatus": {
         "Options": [
            "Submitted",
            "Validating",
            "Scheduled",
            "InProgress",
            "Completed",
            "Aborting",
            "Aborted",
            "UserCancelled",
            "SysRetired",
            "UserCancelledPending"
        ] 
    },
  "ReportFrequency": {
         "Options":  [
            "onDemand",
            "Hourly",
            "Daily",
            "Weekly",
            "Monthly",
            "Annually"
        ] 
    },
  "intervalDuration":316224000000000,
  "RequestId":"Moy/IpfPA0SLUHNYt54q4w==",
  "lastInstanceId":"AAAAAAAAAAAAAAAAAAAAAA==",
  "accountIds":[1]
 }
```

Similar objects are returned for **Generate\~Report** and **Schedule\~Report** calls. As a result, for an on-demand **Generate\~Report** call, some string-value pairs such as _initialRunTime_ may return the current time and _ReportFrequency_ will always return _OnDemand_ because the report is only generated once and on demand.

| Key               | Value                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| RequestingUser    | **integer.** The User ID of the person requesting the trade activity report. This confirms the ID of the authenticated user who made the request by returning it as part of the response.                                                                                                                                                                                                                                                                                                                                                                                                     |
| OMSId             | **integer.** The ID of the Order Management System on which the trade activity report will be run.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| reportFlavor      | <p><strong>string.</strong> The type of report to be generated. One of:<br>TradeActivity<br>Transaction<br>Treasury<br><br>The <em>reportFlavor</em> string confirms the nature of the call.</p>                                                                                                                                                                                                                                                                                                                                                                                              |
| createTime        | **string.** The time and date on which the request for the trade activity report was made.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| initialRunTime    | **string.** The time and date at which the trade activity report was first run.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| intervalStartTime | **string.** The start of the period that the report will cover.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| intervalEndTime   | **string.** The end of the period that the report will cover.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| RequestStatus     | <p><strong>string.</strong> The status of the request for the trade activity report. A Generate~Report request will always return <em>Submitted</em>. Each request returns one of:<br>Submitted<br>Validating<br>Scheduled<br>InProgress<br>Completed<br>Aborting<br>Aborted<br>UserCancelled<br>SysRetired<br>UserCancelled<br>Pending</p>                                                                                                                                                                                                                                                   |
| ReportFrequency   | <p><strong>string.</strong> When the report runs. For a <strong>Generate~Report</strong> call, this is always OnDemand. One of:<br>OnDemand<br>Hourly<br>Daily<br>Weekly<br>Monthly<br>Annually</p>                                                                                                                                                                                                                                                                                                                                                                                           |
| intervalDuration  | <p><strong>long integer.</strong> The period that the report covers relative to the run date. The <strong>Generate~Report</strong> call requires a start time and an end time. The AlphaPoint software calculates the difference between them as <em>intervalDuration</em>.<br><br>For example, say that you specify a 90-day start-date-to-end-date window for a report. The <em>intervalDuration</em> value returns a value equivalent to 90 days. If you have called <strong>Generate~Report</strong>, that value simply confirms the length of time that the on-demand report covers.</p> |
| RequestId         | **string.** The ID of the original request. Request IDs are long strings unique within the Order Management System.                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| lastInstanceId    | **string.** For scheduled reports, the report ID of the most recent previously run report. Will be _null_ for a **Generate\~Report** call, because generated reports are on-demand.                                                                                                                                                                                                                                                                                                                                                                                                           |
| accountIds        | **integer array.** A comma-delimited array of account IDs whose trades are reported in the trade activity report.                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
