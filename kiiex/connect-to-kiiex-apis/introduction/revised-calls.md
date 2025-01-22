# Revised calls

### Revised Calls 3.4.1 <a href="#revised-calls-3-4-1" id="revised-calls-3-4-1"></a>

**SendOrder**

Request Payload changed for Market Buy Value - if Buy order and Value (decimal) parameter is supplied, the Market order will execute up to the value specified.

**GetExchangeServiceIds**

> Old GetExchangeServiceIDs Response An array of strings representing service ids.
>
> New GetExchangeServiceIds Response Array hard coded with a single entry: "Matching Engine"

```
[
    {
        "Name": "V2ExchangeCore|1",
        "ServiceId": "Matching Engine"
        "URI": null
    }
]
```

**GetExchanges**

> Old GetExchangeServiceIds Response A list of exchanges within a specified exchange service id.
>
> New GetExchangeServiceIds Response Retrieves exchanges from "THE" mathcing engine as there can only ever be one as of 3.4

**Validate2FA**

Behavior change, no longer has public permissions specified.

**AddInstrument (DEPRECATED)**

Behavior change, endpoint returns with bad request message specifying the endpoint is deprecated.

**UpdateInstrument (DEPRECATED)**

Behavior change, endpoint returns with bad request message specifying the endpoint is deprecated.

**RemoveOperatorUser**

Behavior change from “Deprecated” to “Remove Association of Operator with User"
