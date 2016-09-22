# Transactions

## Archive

Transactions are automatically archived by the server. During the weekly deduction, if a Transaction belongs to the previous month, it is archived. This allows Transactions to be included in the weekly deduction without being prematurely archived.

Archiving is designed to appear like the Transaction was essentially deleted, but avoids several pitfalls of deleting transactions every month, namely:

1. Analytics on past Transaction data.
2. Pulling in new Transactions from Plaid after they had already been deleted (in which case there would be no other way to know we had already pulled in that Transaction).

Behind the scenes, archiving is simply the act of setting a boolean flag, but the rest of the server processing is designed to hide this from the client API for the most straightforward experience. Regardless, it has been included in the API documentation because it occasionally comes up during topics like error handling or analytics.

## Back Out

```shell
curl _X POST "...v1/transactions/:id/back_out"
  -H "Authorization: TOKEN"
```

> Successful response:

```json
{
  "id":"9bf406fc-cc64-45e2-b536-df9f1b0caa4a",
  "date":"2014-06-23",
  "amount":"2307.15",
  "name":"Apple Store",
  "category_id":"19013000",
  "created_at":"2016-02-19T11:24:33.873-08:00",
  "updated_at":"2016-02-19T11:24:33.873-08:00",
  "invested":false,
  "backed_out":true,
  "amount_invested":"0.0",
  "account_id":"3dce9e2f-5321-431d-bd67-9ab3db32a4d3",
  "vice":"Electronics"
}
```

> Validation errors

```json
{
  "transaction":[
    "has already been archived",
    "has already been invested"
  ]
}
```

Flags a given transaction as "backed out", meaning that when it comes time to deduct money from the user's account to deposit into their fund, the target transaction will be skipped. If a transaction has been archived or invested, it cannot be backed out.

### HTTP Request

`POST ...v1/transactions/:id/back_out`

### Response

Parameter | Description
--------- | -----------
:id | The ID of the Transaction

## Restore

```shell
curl _X POST "...v1/transactions/:id/restore"
  -H "Authorization: TOKEN"
```

> Successful response:

```json
{
  "id":"9bf406fc-cc64-45e2-b536-df9f1b0caa4a",
  "date":"2014-06-23",
  "amount":"2307.15",
  "name":"Apple Store",
  "category_id":"19013000",
  "created_at":"2016-02-19T11:24:33.873-08:00",
  "updated_at":"2016-02-19T11:24:33.873-08:00",
  "invested":false,
  "backed_out":false,
  "amount_invested":"0.0",
  "account_id":"3dce9e2f-5321-431d-bd67-9ab3db32a4d3",
  "vice":"Electronics"
}
```

> Validation errors

```json
{
  "transaction":[
    "has already been archived",
    "has already been invested"
  ]
}
```

The opposite of backing out of a transaction. This endpoint re-flags a given transaction as "not backed out", meaning that when it comes time to deduct money from the user's account to deposit into their fund, the target transaction will be invested at a percentage given by User.invest_percent. If a transaction has been archived or invested, it cannot be restored.

### HTTP Request

`POST ...v1/transactions/:id/restore`

### Response

Parameter | Description
--------- | -----------
:id | The ID of the Transaction
