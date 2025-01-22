# Deposit and Withdraw Templates

Templates provide a set of information about banking tasks during deposits and withdrawals in the form of specific key-value pairs. Each template has a name. There are different templates for different types of deposit and withdrawal, determined by the product or asset (BitCoin, Monero, US Dollar, etc.), the specific bank or other Account Provider, and the information that the Account Provider requires for the transaction.

Most templates are used for withdrawals.

Example 1 and 2 are two example templates.

> \
> Template Example 1

```
"TemplateformType": "Standard",
{
    "Full Name": "John Smith",
    "Language": "en",
    "Comment": "",
    "BankAddress": "123 Fourth St.",
    "BankAccountNumber": "12345678",
    "BankAccountName": "John Smith & Sons",
    "Swiftcode": "ABCDUSA1"
}
```

> Template Example 2

```
"TemplateFormType": "TetherRPCWithdraw",
{
    "TemplateType": "TetherRPCWithdraw",
    "Comment": "TestWithdraw",
    "ExternalAddress": "ms6C3pKAAr8gRCcnVebs8VRkVrjcvqNYv3"
}
```

The content of the template depends on the Account Provider that you use for deposits and withdrawals. The Account Provider does not supply the template _per se_ (they do, however, determine the fields that are in the template). The template is specific to each Account Provider.

To determine which withdrawal template types are available to you, call **GetWithdrawTemplateTypes.**
