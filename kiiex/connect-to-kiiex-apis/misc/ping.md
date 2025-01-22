# Ping

**Category:** User\
**Permissions:** Public\
**Call Type:** Synchronous

Used to keep a connection alive.

#### Request <a href="#request" id="request"></a>

```
{ }
```

Ping requires no payload.

#### Response <a href="#response" id="response"></a>

```
{
  "msg": "PONG"
}
```

Response is PONG.

| Key | Value            |
| --- | ---------------- |
| msg | **string.** PONG |
