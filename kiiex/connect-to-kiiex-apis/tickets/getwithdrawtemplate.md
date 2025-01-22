# GetWithdrawTemplate

**Category:** System\
**Permissions:** Operator, Withdraw\
**Call Type:** Synchronous

Returns the text of the specific withdrawal template. To find out what templates are available to you, call **GetWithdrawTemplateTypes.**

#### Request <a href="#request" id="request"></a>

```
{
    "OMSId": 1,
    "ProductId": 1,
    "TemplateType": "Template Name",
    "AccountId": 1,
    "AccountProviderId": 1
}
```

The system "knows" which Account Provider's withdrawal template to return based on the product ID and the template name you provide. There is usually only one Account Provider per product on an Exchange. _AccountId_ and _AccountProviderId_ therefore are optional key-value pairs.

| Key               | Value                                                                                             |
| ----------------- | ------------------------------------------------------------------------------------------------- |
| OMSId             | **integer.** REQUIRED The ID of the Order Management System on which the withdrawal will be made. |
| ProductId         | **integer.** REQUIRED The ID of the product (asset) about to be withdrawn.                        |
| TemplateType      | **string.** REQUIRED The name of the withdrawal template you want to return.                      |
| AccountId         | **integer.** OPTIONAL The ID of the account from which you plan to make the withrawal.            |
| AccountProviderId | **integer.** OPTIONAL The ID of the Account Provider you plan to use for the withdrawal.          |

#### Response <a href="#response" id="response"></a>

```
{
    "Template": "",
    "result": true,
    "errormsg": "",
    "statuscode": 0
}
```

The Response returns the key-value pairs of the template, along with any error messages about the call. The text of the template will vary from Account Provider to Account Provider.

| Key        | Value                                                                                                                                                                                                                                                                                                                                                                           |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Template   | **string.** The key-value pairs of the template inside a JSON string.                                                                                                                                                                                                                                                                                                           |
| result     | **Boolean.** Returns _true_ if the call is successfully received; otherwise _false._                                                                                                                                                                                                                                                                                            |
| errormsg   | <p><strong>string.</strong> A successful receipt of the call returns <em>null.</em> The <em>errormsg</em> for an unsuccessful call returns one of:<br>Not Authorized (errorcode 20)<br>Invalid Request (errorcode 100)<br>Operation Failed (errorcode 101)<br>Server Error (errorcode 102)<br>Resource Not Found (errorvode 104)<br>Operation Not Supported (errorcode 106)</p> |
| statuscode | <p><strong>integer.</strong> If <em>result</em> is <em>false</em>, <em>statuscode</em> can return:<br><strong>32</strong> Not Authorized<br><strong>33</strong> AssetManager_Not_Found<br><br>If no Account Provider is located, <em>statuscode</em> returns <em>null.</em></p>                                                                                                 |
