# GetOmsFeeTiers

**Category:** User\
**Permissions:** Operator\
**Call Type:** Synchronous

Gets a list of fees specified on an Instrument

#### Request <a href="#request" id="request"></a>

```
{
  "omsId": 1,
  "instrumentId": 1
}
```

| Key          | Value                                                                                    |
| ------------ | ---------------------------------------------------------------------------------------- |
| omsId        | **integer**. The ID of the Order Management System on which the instrument is available. |
| instrumentId | **integer**. The ID of the instrument.                                                   |

#### Response <a href="#response" id="response"></a>

```
[
    {
        "omsId": 0,
        "accountId": 0,
        "instrumentId": 0,
        "orderType": "Unknown",
        "feeId": 0,
        "feeAmt": 0,
        "feeCalcType": "Percentage",
        "feeType": "Flat",
        "ladderThreshold": 0,
        "ladderSeconds": 0,
        "isActive": true,
    },
]
```

The response for **GetInstruments** is an array of objects listing all the instruments available on the Order Management System.

| Key             | Value                                                                                                                  |
| --------------- | ---------------------------------------------------------------------------------------------------------------------- |
| omsId           | **integer.** The ID of the Order Management System on which the fee is defined.                                        |
| instrumentId    | **integer.** The ID of the instrument on which the fee is defined.                                                     |
| accountId       | **integer.** The ID of the account on which the fee is defined.                                                        |
| orderType       | **string.** The type of order on which the fee is defined.                                                             |
| feeId           | **integer.** The ID of the fee.                                                                                        |
| feeAmt          | **decimal.** The amount to be used in the calculation of the fee.                                                      |
| feeCalcType     | **string.** The calculation type for the fee. One of FlatRate or Percentage.                                           |
| feeType         | **string.** The type of fee. Flat, Ladder, Exemption, AdminFee, AffiliateFee, MakerFee, TakerFee, or FlatPegToProduct. |
| ladderThreshold | **decimal.**                                                                                                           |
| ladderSeconds   | **long integer.**                                                                                                      |
| isActive        | **boolean.** If the fee is active or not.                                                                              |
