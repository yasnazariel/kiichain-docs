# SubmitDepositTicketComment

**Category:** System\
**Permissions:** Operator, Trading\
**Call Type:** Synchronous

Creates a comment and attaches that comment to a specific deposit ticket.

#### Request <a href="#request" id="request"></a>

```
{
    "commentId": 0,
    "enteredBy": 0,
    "enteredDateTime": "0001-01-01T00:00:00",
    "comment": "",
    "operatorId": 0,
    "omsId": 0,
    "ticketCode": "43d1a9f0-8dc3-46f9-b457-297c800d8c9c",
    "ticketId": 0
}
```

| Key             | Value                                                                                                                                                                                                                                                      |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| commentId       | **integer.** The ID of this specific comment. In the Request, set this to 0. The Response supplies the system-assigned value for _commentId._                                                                                                              |
| enteredBy       | **integer.** The user ID of the user making the comment. If an operator (admin) is making the request, this should be the generic user ID of the admin (not the operator ID).                                                                              |
| enteredDateTime | **string.** The date and time that the comment was created, in Microsoft Ticks format and UTC time.                                                                                                                                                        |
| comment         | **string.** The comment string itself.                                                                                                                                                                                                                     |
| operatorId      | **integer.** The ID of an operator (admin) making the comment. The value for _operatorId_ should be available programmatically from the ticket being commented.                                                                                            |
| omsId           | **integer.** The ID of the Order Management System on which the deposit is being made.                                                                                                                                                                     |
| ticketCode      | **string.** A GUID (globally unique identifier) that identifies the deposit ticket to which the comment is attached. The value for _ticketCode_ should be available programmatically from the ticket being commented.                                      |
| ticketId        | **integer.** An ID assigned by the system to the ticket. You can obtain this value from the calls **CreateDepositTicket,** **GetAllDepositTickets,** **GetDepositTicket,** and **GetDepositTickets.** In all these calls, the key is named _ticketNumber._ |

#### Response <a href="#response" id="response"></a>

```
{
    "success": true,
    "commentid": 10000002
}
```

| Key       | Value                                                                                                                                                 |
| --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| success   | **Boolean.** A _true_ value means that the comment has been successfully attached to the deposit ticket; _false_ means that it has not been attached. |
| commentId | **integer.** The ID assigned by the system to this specific comment.                                                                                  |
