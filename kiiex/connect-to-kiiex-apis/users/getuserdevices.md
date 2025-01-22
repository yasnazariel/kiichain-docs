# GetUserDevices

**Category:** System\
**Permissions:** Operator, Trading\
**Call Type:** Synchronous

Gets the Registered Device trail for the current session. Given the userId, action, date range or all 3

#### Request <a href="#request" id="request"></a>

```
{
    "UserId": 1
}
```

| Key    | Value                                                         |
| ------ | ------------------------------------------------------------- |
| UserId | **integer.** The user ID of the user requesting user devices. |

#### Response <a href="#response" id="response"></a>

```
[
    {
        "HashCode": 1,
        "Location": "location",
        "DeviceName": "name",
        "IpAddress": "127.0.0.0",
        "UserId": 1,
        "IsTrusted": true,
        "ExpirationTime": 637020116076891148
    }
]
```

The Response is an array of devices associated with the user.

| Key            | Value                                                              |
| -------------- | ------------------------------------------------------------------ |
| HashCode       | **integer.** Hash code associated with the device.                 |
| Location       | **string.** Location of device                                     |
| DeviceName     | **string.** Name of device                                         |
| IpAddress      | **string.** IP address associated with the device                  |
| UserID         | **integer.** User ID associated with the device                    |
| IsTrusted      | **boolean.** If _true_, device is linked with location/ip address. |
| ExpirationTime | **long integer.** Epoch time when device registration expires      |
