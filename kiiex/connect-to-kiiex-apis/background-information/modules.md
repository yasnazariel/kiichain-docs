# Modules

The KIIEX software consists of several modules that include the Order Management System (OMS), the matching engine, and the Asset Manager. During installation, each is assigned an ID.

The Order Management System is the mechanism that manages access to the trading venue. The OMS controls permissions, accounts, and users. The OMS must be specified in many calls.

The order book resides on the AlphaPoint matching engine.

A trading venue is a combination of OMS and matching engine that creates a place to access the market and trade. A venue maintains its order book and matching engine, and may access several Order Management Systems.

The Asset Manager controls the deposit and withdrawal of funds belonging to an account. These funds can be denominated in any product that the trading venue allows.
