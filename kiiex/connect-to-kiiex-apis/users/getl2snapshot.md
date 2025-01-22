# GetL2Snapshot

**Category:** User\
**Permissions:** Public\
**Call Type:** Synchronous

Provides a current Level 2 snapshot of a specific instrument trading on an Order Management System to a user-determined market depth. The Level 2 snapshot allows the user to specify the level of market depth information on either side of the bid and ask.

Depth in this call is "depth of market," the number of buyers and sellers at greater or lesser prices in the order book for the instrument.

#### Request <a href="#request" id="request"></a>

```
{
  "OMSId": 1,
  "InstrumentId": 1,
  "Depth": 100 
}
```

| Key          | Value                                                                                                                                                  |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| OMSId        | **integer**. The ID of the Order Management System where the instrument is traded.                                                                     |
| InstrumentId | **integer**. The ID of the instrument that is the subject of the snapshot.                                                                             |
| Depth        | **integer**. Depth of the market — the number of buyers and sellers at greater or lesser prices in the order book for the instrument. Defaults to 100. |

#### Response <a href="#response" id="response"></a>

```
[
    [       
        1, // Account Id
        123,// ActionDateTime in Posix format X 1000
        0,   // ActionType 0 (New), 1 (Update), 2(Delete)
        0.0, // LastTradePrice
        0, // OrderId
        0.0, //Price
        0,  // ProductPairCode
        0.0, // Quantity
        0, // Side
    ],
]

// This is how the response is sent:

[[1,123,0,0.0,0,0.0,0,0.0,0]]
```

The response is an array of elements for one specific instrument, the number of elements corresponding to the market depth specified in the Request. It is sent as an uncommented, comma-delimited list of numbers. The example is commented. The _Level2UpdateEvent_ contains the same data, but is sent by the OMS whenever trades occur. To receive _Level2UpdateEvents_, a user must subscribe to _Level2UpdateEvents_.

| Key             | Value                                                                                                                                                                                               |
| --------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Account Id      | **integer**. Number to identify account.                                                                                                                                                            |
| ActionDateTime  | **long integer.**. _ActionDateTime_ identifies the time and date that the snapshot was taken or the event occurred, in POSIX format X 1000 (milliseconds since 1 January 1970).                     |
| ActionType      | <p><strong>integer</strong>. L2 information provides price data. This value shows whether this data is:<br><strong>0</strong> new<br><strong>1</strong> update<br><strong>2</strong> deletion</p>   |
| LastTradePrice  | **real**. The price at which the instrument was last traded.                                                                                                                                        |
| Order Id        | **integer**. Number to identify order.                                                                                                                                                              |
| Price           | **real**. Bid or Ask price for the Quantity (see _Quantity_ below).                                                                                                                                 |
| ProductPairCode | **integer**. _ProductPairCode_ is the same value and used for the same purpose as _InstrumentID_. The two are completely equivalent. _InstrumentId_ 47 = _ProductPairCode_ 47.                      |
| Quantity        | **real**. Quantity available at a given Bid or Ask price (see _Price_ above).                                                                                                                       |
| Side            | <p><strong>integer</strong>. One of:<br><strong>0</strong> Buy<br><strong>1</strong> Sell<br><strong>2</strong> Short (reserved for future use)<br><strong>3</strong> Unknown (error condition)</p> |
