# Behavior Changes

**API Behavior Changes**

Any query APIs that return these objects now have the below new fields and response value changes as listed.

**AccountPosition**

| Key                        | Value                                                      |
| -------------------------- | ---------------------------------------------------------- |
| NotionalHoldAmount         | **decimal.** Cross Product Amount on Hold from open orders |
| NotionalRate               | **decimal.** Current notional rate from base currency      |
| TotalDayDepositNotional    | **decimal.** Total Calendar Day Deposit Notional           |
| TotalMonthDepositNotional  | **decimal.** Total Calendar Month Deposit Notional         |
| TotalDayWithdrawNotional   | **decimal.** Total Calendar Day Withdraw Notional          |
| TotalMonthWithdrawNotional | **decimal.** Total Calendar Month Withdraw Notional        |

**OrderTrade**

| Key                      | Value                                                                  |
| ------------------------ | ---------------------------------------------------------------------- |
| CounterPartyClientUserId | **int.** Indicates counterparty source of trade (OMS, Remarketer, FIX) |
| NotionalProductId        | **int.** Notional product the notional value was captured in           |
| NotionalRate             | **decimal.** Notional rate from base currency at time of trade         |
| NotionalValue            | **decimal.** Notional value in base currency of venue at time of trade |

**AccountInstrumentStatistics**

| Key                        | Value                                                        |
| -------------------------- | ------------------------------------------------------------ |
| NotionalProductId          | **int.** Notional product the notional value was captured in |
| DailyNotionalTradeVolume   | **decimal.** Total Calendar Day Trading Notional             |
| MonthlyNotionalTradeVolume | **decimal.** Total Calendar Month Trading Notional           |
| YearlyNotionalTradeVolume  | **decimal.** Total Calendar Year Trading Notional            |

**VerificationLevelInstruments**

| Key                  | Value                                                        |
| -------------------- | ------------------------------------------------------------ |
| NotionalProductId    | **int.** Notional product the notional value was captured in |
| DailyNotionalLimit   | **decimal.** Total Calendar Day Trading Notional             |
| MonthlyNotionalLimit | **decimal.** Total Calendar Month Trading Notional           |
| YearlyNotionalLimit  | **decimal.** Total Calendar Year Trading Notional            |

**AccountStatistics**

| Key                        | Value                                               |
| -------------------------- | --------------------------------------------------- |
| TotalDayDepositNotional    | **decimal.** Total Calendar Day Deposit Notional    |
| TotalMonthDepositNotional  | **decimal.** Total Calendar Month Deposit Notional  |
| TotalDayWithdrawNotional   | **decimal.** Total Calendar Day Withdraw Notional   |
| TotalMonthWithdrawNotional | **decimal.** Total Calendar Month Withdraw Notional |

**VerificationLevelProducts**

| Key                          | Value                                                     |
| ---------------------------- | --------------------------------------------------------- |
| DailyDepositNotionalLimit    | **decimal.** Total Calendar Day Deposit Notional Limit    |
| MonthlyDepositNotionalLimit  | **decimal.** Total Calendar Month Deposit Notional Limit  |
| DailyWithdrawNotionalLimit   | **decimal.** Total Calendar Day Withdraw Notional Limit   |
| MonthlyWithdrawNotionalLimit | **decimal.** Total Calendar Month Withdraw Notional Limit |

**OMSInfo**

| Key                   | Value                                                     |
| --------------------- | --------------------------------------------------------- |
| BaseNotionalProductId | **int.** Id of Base Product to be used in Notional Limits |

**Fee**

| Key     | Value                                                                                                      |
| ------- | ---------------------------------------------------------------------------------------------------------- |
| FeeTier | **int.** Id of the Fee Tier the fee belongs to. Matches AccountInfo FeeGroupId (previously existing field) |

**Instrument**

| Key                                 | Value                                                                                                                                                                                             |
| ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| PriceCollarIndexDifference          | **decimal.** The percent different from the index price that an order is allowed to execute at. Anything falling outside of the index price +/- (1 + PriceCollarIndexDifference) will be collared |
| PriceCollarConvertToOtcEnabled      | **bool.** Turns on/off conversion of collared orders to block trades                                                                                                                              |
| PriceCollarConvertToOtcClientUserId | **int.** Internal System UserId to assign the collared otc orders to. Should alwaays be 1 in current implementation (default)                                                                     |
| PriceCollarConvertToOtcAccountId    | **int.** Account Id to assign the collared orders to. This will effectively be a liability account that will need to have working block trades managed by operator.                               |
| PriceCollarConvertToOtcThreshold    | **decimal.** Threshold of remaining size of order to convert to block trade. If collared order does not have remaining quantity above this threshold the remainder will be cancelled.             |
| OtcConvertSizeEnabled               | **bool.** Turns on/off auto conversion of 'large' limit orders converted to block trade orders upon receipt by the matching engine                                                                |
| OtcConvertSizeThreshold             | **decimal.** Threshold to convert limit order quantity to block trade automatically for discovery by block trade market participants                                                              |
