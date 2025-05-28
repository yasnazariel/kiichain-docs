# Quotes and Orders

The KIIEX API includes calls related to both quotes and orders. Quoting is not enabled for the retail end user of AlphaPoint software. Only registered market participants or marketmakers may quote. Your trading venue may offer quotes separately from orders.

* A quote expresses a willingness to buy or sell at a given price.
* An order is a directive to buy or sell.

In this version of the AlphaPoint matching engine software, quotes and orders are synonymous. They both can buy or sell. This is because the matching engine (like most matching engines) requires a "firm quote" — a guaranteed bid or ask.

For both quotes and orders, trading priority is the same, and no preference is given one over the other. In code, the matching engine flags a quote for eventual regulatory and compliance rules, but for current software operation and trade execution, quotes and orders behave equivalently.

#### Best Practices/Quotes and Orders <a href="#best-practices-quotes-and-orders" id="best-practices-quotes-and-orders"></a>

Use the order-related API calls in preference to quote-related calls unless you specifically require quote-related calls.
