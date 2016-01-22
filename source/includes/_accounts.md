# Accounts

## Get a Specific Account

```shell
curl "...api/v1/accounts/1"
  -H "Authorization: TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "id": 1,
  "user_id": 2,
  "acctNum": "1112223333",
  "routNum": "123456789",
  "cardNum": "4242424242424242",
  "cardName": "My Debit",
  "expMonth": 1,
  "expYear": 2018,
  "zipcode": "90000"
}
```

Retrieves a specific account.

### HTTP Request

`GET ...api/v1/accounts/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the account to retrieve
