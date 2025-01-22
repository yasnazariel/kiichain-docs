# GetUnredactedUserConfigByKey

**Category:** System\
**Permissions:** Operator, Trading\
**Call Type:** Synchronous

Gets an unredacted config for a user config

#### Request <a href="#request" id="request"></a>

```
{
    "userId": 0,
    "userName": "",
    "key" : ""
}
```

| Key      | Value                                                                                                                                                                                                                |
| -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| userId   | **integer.** The ID of the user whose configuration key-value pairs you want to return.                                                                                                                              |
| userName | **string.** The user name of the user whose configuration key-value pairs you want to return.                                                                                                                        |
| key      | **string.** The "key" in the payload represents the specific configuration key that you want to retrieve for the user. It is used to specify which unredacted configuration setting you are interested in obtaining. |

#### Response <a href="#response" id="response"></a>

```
[
    {
        "Key": "Config1",
        "Value": "Config1Val"
    }
]
```

The Response returns an array of a variable number of elements, depending on the needs of the Exchange.

| Key   | Value                                                                         |
| ----- | ----------------------------------------------------------------------------- |
| Key   | **string.** The name of the key part of the key-value pair.                   |
| Value | **string.** The value part of the key-value pair. The value must be a string. |

\
