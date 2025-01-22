# GetAllDepositRequestInfoTemplates

**Category:** System\
**Permissions:** Operator, Trading\
**Call Type:** Synchronous

Returns an array of all templates available to the caller that describe a deposit form for a specific product.

An Account Provider may require specific deposit information. Deposit templates answer than need.

#### Request <a href="#request" id="request"></a>

```
{
    "OMSId": 1,
    "ProductId": 1
}
```

| Key       | Value                                                                              |
| --------- | ---------------------------------------------------------------------------------- |
| OMSId     | **integer.** The ID of the Order Management System on which the product is traded. |
| ProductId | **integer.** The ID of the product to be deposited.                                |
|           |                                                                                    |

#### Response <a href="#response" id="response"></a>

```
[
    {
        "Template": {
            "ProviderType": "BitcoinRpc",
            "Template": "{}",
            "ProcessInfo": "",
            "UseGetDepositWorkflow": true,
            "DepositWorkflow": "CryptoWallet"
            },
        "result": true,
        "errormsg": null,
        "statuscode": 0
    },
]
```

The Response is an array of information for templates appropriate to the product specified in the Request and available to the caller, along with fields that show whether the Response successfully returned the Template information. The key-value pairs of the inner Template object vary from Account Provider to Account Provider.

**Template object**

| Key                   | Value                                                                                                                                                                                                                                                      |
| --------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ProviderType          | <p><strong>String.</strong> The type of asset handled by the Account Provider. Possible values are:<br><br>BitcoinRpc<br>BitGoRpc<br>Internal Accounting<br>WsAccountingProvider<br>EthereumERC20<br>EthereumRPC</p>                                       |
| Template              | **JSON object.** The key-value pairs of _Template_ vary from Account Provider to Account Provider.                                                                                                                                                         |
| ProcessInfo           | **String.** The _ProcessInfo_ string varies with the Account Provider and the asset being deposited. In a generic deposit template, the _ProcessingInfo_ key-value pair is empty; in other cases it is an address for processing the deposit.              |
| UseGetDepositWorkflow | **Boolean.** A _true_ value causes the deposit to use the deposit workflow named in _DepositWorkflow._ A _false_ value causes the deposit not to use that defined workflow.                                                                                |
| DepositWorkflow       | <p><strong>String.</strong> A set of defined workflows for this template. The workflows are defined and named during the installation of the Exchange. Choices are:<br><br>CryptoWallet<br>ManualDeposit<br>MerchantForm<br>MerchantRedirect<br>Custom</p> |

**Response fields**

| Key        | Value                                                                                                                                                                                                                                                                                                                                                                               |
| ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| result     | **Boolean.** If the call has been successfully received by the Order Management System, returns _true,_ otherwise returns _false._                                                                                                                                                                                                                                                  |
| errormsg   | <p><strong>String.</strong> A successful receipt of the call returns <em>null.</em> The <em>errormsg</em> key for an unsuccessful call can return:<br><br>Not Authorized (errorcode 20)<br>Invalid Request (errorcode 100)<br>Operation Failed (errorcode 101)<br>Server Error (errorcode 102)<br>Resource Not Found (errorcode 104)<br>Operation Not Supported (errorcode 106)</p> |
| statusCode | <p><strong>integer.</strong> If <em>result</em> is <em>false,</em> <em>statusCode</em> can return:<br><br><strong>32</strong> Not Authorized<br><strong>33</strong> Asset_Manager_Not_Found<br><br>If no Account Provider is located, <em>statusCode</em> returns <em>null.</em></p>                                                                                                |
