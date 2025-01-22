# Users, Accounts, and Permissions

KIIEX software differentiates between _user_ and _account_. A user is the person who logs in; an account represents the funds and trading that the user does — much like a bank account represents funds and checks.

As with a bank account, an individual user may have multiple Exchange accounts. Similarly, multiple users may trade through a single account. There may be users who have trading access to one set of accounts that overlap (but do not duplicate) the set of accounts that another user can access. There may be a many-to-many relationship where two or more users have access to a set of accounts.

The use case for this kind of "joint tenancy" is an active trading desk where a specific individual may not always be present. If User A will not be present, User B can monitor and trade on the market. User A may wish to cancel his pending trades for a specific account or instrument, but not those of his trading partner under the same account or for the same instrument.

Permissions handle the rules that determine what a user can access and do with orders, cancellations, and the other tasks of a trading venue. Most permissions encompass tasks such as trading, depositing, or withdrawing funds; but a permission can be set for each API call for each individual in the venue.

An administrator with Operator permission sets up a user's permissions on the OMS when the user joins the trading venue, and only an administrator with Operator permission or above can change them. A full discussion of permissions is not part of this API.
