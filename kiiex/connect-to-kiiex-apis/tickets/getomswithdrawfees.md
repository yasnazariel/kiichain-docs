# GetOMSWithdrawFees

**Category:** System\
**Permissions:** Operator, Withdraw\
**Call Type:** Synchronous

Returns an array of objects, each of which describe a fee assessed on a specific product (asset).

#### Request <a href="#request" id="request"></a>

```
{
    "OMSId": 1,
    "ProductId": 1
}
```

| Key       | Value                                                                                      |
| --------- | ------------------------------------------------------------------------------------------ |
| OMSId     | **integer.** The ID of the Order Management System on which the produce (asset) is traded. |
| ProductId | **integer.** The ID of the product (asset) for which you want a list of fees.              |

#### Response <a href="#response" id="response"></a>

```
[
    {
        "OMSId": 1,
        "AccountId": 0,
        "FeeId": 47,
        "FeeAmt": 1,
        "FeeCalcType": "Percentage",
        "IsActive": false,
        "ProductId": 1
    },
]
```

The Response is an array of objects, each describing a fee.

| Key         | Value                                                                                                                                                                                                                                                                                                          |
| ----------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| OMSId       | **integer.** The ID of the Order Management System on which the product (asset) is traded.                                                                                                                                                                                                                     |
| AccountId   | **integer.** The ID of the account requesting the withdrawal fee information. Withdrawal fees may vary between accounts. The system "knows" the account of the requesting user.                                                                                                                                |
| FeeId       | **integer.** The ID of the fee reported in this object.                                                                                                                                                                                                                                                        |
| FeeAmt      | **real.** The fee assessed for this product. If _FeeCalcType_ is Percentage, this value is the percentage of the fee. If the _FeeCalcType_ is FlatRate, this value is the number of units and fractions of units of the product. The Exchange usually assesses withdrawal fees in the product being withdrawn. |
| FeeCalcType | **string.** The way the fee is calculated, either as a flat rate (FlatRate) or as a percentage (Percentage) of the withdrawal.                                                                                                                                                                                 |
| IsActive    | **Boolean.** A _true_ value signifies that this fee is active for this product; a _false_ value that the fee is not active for this product.                                                                                                                                                                   |
| ProductId   | **integer.** The ID of the product (asset) against which the fee is assessed.                                                                                                                                                                                                                                  |
