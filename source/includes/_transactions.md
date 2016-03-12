# Transactions

## Back Out

```shell
curl _X POST "...api/v1/transactions/:id/back_out"
  -H "Authorization: TOKEN"
```

> Successful response:

```json
{
  "id":1,
  "plaid_id":"KdDjmojBERUKx3JkDdO5IaRJdZeZKNuK4bnKJ1",
  "date":"2014-06-23",
  "amount":"2307.15",
  "name":"Apple Store",
  "category_id":"19013000",
  "account_id":1,
  "created_at":"2016-02-19T11:24:33.873-08:00",
  "updated_at":"2016-02-19T11:24:33.873-08:00",
  "user_id":1,
  "invested":false,
  "backed_out":true,
  "vice":"Electronics"
}
```

> Validation errors

```json
{
  "transaction":[
    "has already been invested"
  ]
}
```

Flags a given transaction as "backed out", meaning that when it comes time to deduct money from the user's account to deposit into their fund, the target transaction will be skipped.

### HTTP Request

`POST ...api/v1/transactions/:id/back_out`

### Response

Parameter | Description
--------- | -----------
:id | The ID of the Transaction

## Invest

```shell
curl _X POST "...api/v1/transactions/:id/invest"
  -H "Authorization: TOKEN"
```

> Successful response:

```json
{
  "id":1,
  "plaid_id":"KdDjmojBERUKx3JkDdO5IaRJdZeZKNuK4bnKJ1",
  "date":"2014-06-23",
  "amount":"2307.15",
  "name":"Apple Store",
  "category_id":"19013000",
  "account_id":1,
  "created_at":"2016-02-19T11:24:33.873-08:00",
  "updated_at":"2016-02-19T11:24:33.873-08:00",
  "user_id":1,
  "invested":false,
  "backed_out":true,
  "vice":"Electronics"
}
```

> Validation errors

```json
{
  "transaction":[
    "has already been invested"
  ]
}
```

The opposite of backing out of a transaction, this endpoint re-flags a given transaction as "not backed out", meaning that when it comes time to deduct money from the user's account to deposit into their fund, the target transaction will be invested at a percentage given by User.invest_percent.

### HTTP Request

`POST ...api/v1/transactions/:id/invest`

### Response

Parameter | Description
--------- | -----------
:id | The ID of the Transaction
