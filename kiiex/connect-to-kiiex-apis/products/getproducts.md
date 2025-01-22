# GetProducts

**Category:** User\
**Permissions:** Public\
**Call Type:** Synchronous

Returns an array of products and currencies available on the exchange. A product is an asset that is tradable or paid out.

#### Request <a href="#request" id="request"></a>

```
{
  "OMSId": 1,
  "GetDisabled" : false
}
```

| Key         | Value                                                                                                                         |
| ----------- | ----------------------------------------------------------------------------------------------------------------------------- |
| OMSId       | **integer.** The ID of the Order Management System for which the array of available products and currencies will be returned. |
| GetDisabled | **boolean**. A boolean flag indicating whether to include disabled products in the response.                                  |

#### Response <a href="#response" id="response"></a>

```
[
    {
        "omsId":0,
        "productId":0,
        "product":"",
        "productFullName":"",
        "productType":0,
        "decimalPlaces":0.0,
        "tickSize":0.0,
        "noFees":false
    },
]
```

The response returns an array of objects, one object for each product available on the Order Management System.

| Key             | Value                                                                                                                                                                                                                                                                 |
| --------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| omsId           | **integer.** The ID of the Order Management System that offers the product.                                                                                                                                                                                           |
| productId       | **long integer.** The ID of the product.                                                                                                                                                                                                                              |
| product         | **string.** “Nickname” or shortened name of the product. For example, NZD (New Zealand Dollar).                                                                                                                                                                       |
| productFullName | **string.** Full and official name of the product. For example, New Zealand Dollar.                                                                                                                                                                                   |
| productType     | <p><strong>integer.</strong> A number describing the nature of the product. One of:<br>0 Unknown (an error condition)<br>1 NationalCurrency<br>2 CryptoCurrency<br>3 Contract</p>                                                                                     |
| decimalPlaces   | **integer.** The number of decimal places in which the product is divided. The maximum is 8. For example, US Dollars are divided into 100 units, or 2 decimal places. Other products may be different. Burundi Francs use 0 decimal places and the Rial Omani uses 3. |
| tickSize        | **real.** The smallest increment in which the product can trade.                                                                                                                                                                                                      |
| noFees          | **Boolean.** Shows whether trading the product incurs transaction fees. The default is _false_; that is, if _NoFees_ is _false_, transaction fees will be incurred. If _NoFees_ is _true_, no fees are incurred.                                                      |
