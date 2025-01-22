# CreateWithdrawTicket

**Category:** System\
**Permissions:** Operator, Withdraw\
**Call Type:** Synchronous

Initiates the withdrawal of funds from an account. You can use **CreateWithdrawTicket** for both cryptocurrency and fiat (national) currencies. The call transfers funds to an external account through a third-party Account Provider accredited by the Exchange.

A user with Withdraw permission can create a withdraw ticket only for an account with which they're associated; a user with Operator permission can create a withdraw ticket for any account.

#### Request <a href="#request" id="request"></a>

```
{
    "OMSId": 1,
    "AccountId": 1,
    "ProductId": 1,
    "Amount": 100.00,
    "TemplateForm": {},
    "TemplateType": "Template Form Type"
}
```

Part of the process of withdrawing an asset (product) is to specify the withdrawal template that sends the asset to the correct destination, usually an Account Provider. The content of templates varies from Account Provider to Account Provider. Get a list of templates available to you by calling **GetWithdrawTemplateTypes.** For more information on templates, see "Deposit and withdraw templates" at the beginning of the Tickets section.

| Key          | Value                                                                                                                                                                                                           |
| ------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| OMSId        | **integer.** The ID of the Order Management System from which the withdrawal is being made.                                                                                                                     |
| AccountId    | **integer.** The ID of the account from which the asset is being withdrawn.                                                                                                                                     |
| ProductId    | **integer.** The ID of the product (or asset) begin withdrawn; the terms are used interchangeably.                                                                                                              |
| Amount       | **real.** The number of units or fractions of units of the asset being withdrawn (not the asset's monetary value). For example. 2.5 BitCoin or 2000.00 US Dollars.                                              |
| TemplateForm | **object.** The contents of the template form vary from Account Provider to Account Provider, depending on the asset being withdrawn and the identity of the Account Provider. See Example 1, below.            |
| TemplateType | **string.** The name of the withdrawal template that controls the destination of the asset being withdrawn. To get a list of withdrawal templates that are available to you, call **GetWithdrawTemplateTypes.** |

**Example 1**

> Example 1: a typical withdrawal template

```
{
    "TemplateType": "ToExternalBitCoinAddress",
    "Comment": "",
    "ExternalAddress": "54123214"
}
```

Example 1 shows a typical withdrawal template.

#### Response <a href="#response" id="response"></a>

> The Response

```
{
    "result": true,
    "errormsg": "Invalid Request",
    "errorcode": 100,
    "detail": "Insufficient Balance"
}
```

The response to **CreateWithdrawTicket** is a standard response object confirming receipt or non-receipt of the information, and does not confirm the ticket _per se._ To view and confirm the ticket was created properly, use the call **GetWithdrawTicket.**

| Key       | Value                                                                                                                                                                                                                                                                                                                                                            |
| --------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| result    | **Boolean.** Field is _true_ if the call has been successfully received by the Order Management System; otherwise _false._                                                                                                                                                                                                                                       |
| errormsg  | <p><strong>string.</strong> A successful receipt of the call returns <em>null.</em> The <em>errormsg</em> value for an unsuccessful call returns one of the following messages:<br>Not Authorized (errorcode 20)<br>Invalid Request (errorcode 100)<br>Operation Failed (errocode 101)<br>Server Error (errorcode 102)<br>Resource Not Found (errorcode 104)</p> |
| errorcode | **integer.** A successful receipt of the call returns 0. An unsuccessful receipt of the call returns one of the _errorcodes_ shown in the _errormsg_ list.                                                                                                                                                                                                       |
| detail    | **string.** Message text that the system may send. Often _null._                                                                                                                                                                                                                                                                                                 |
