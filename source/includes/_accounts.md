# Accounts

## Get Accounts

```shell
curl "...api/v1/accounts"
  -H "Authorization: TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "id": 1,
  "user_id": 2,
  "plaid_id": "mjj9jp92z2fD1mLlpQYZI1gAd4q4LwTKmBNLz",
  "name": "My Savings",
  "institution": "my_institution",
  "available_balance": 1234.56,
  "current_balance": 1234.56,
  "account_num": "9900009606",
  "routing_num": "021000021",
  "account_type": "depository",
  "account_subtype": "savings",
  "created_at": "2016-01-01T01:00:00.000Z",
  "updated_at": "2016-01-02T01:00:00.000Z"
}
```

Retrieves all accounts for the authenticated User.

### HTTP Request

`GET ...api/v1/accounts`

### Response

Parameter | Description
--------- | -----------
user_id | The ID of the Dimention User
plaid_id | The ID of the account on Plaid's server
name | The general name of the account
institution | Plaid's name for this institution
available_balance | The current balance less any outstanding holds or debits
current_balance | Total available funds in the account
account_num | Account number
routing_num | Routing number
account_type | Type of account according to Plaid
account_subtype | More specific type of account
