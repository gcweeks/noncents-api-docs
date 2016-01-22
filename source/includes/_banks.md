# Banks

## Get a Specific Bank

```shell
curl "...api/v1/banks/3"
  -H "Authorization: TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "id": 3,
  "name": "Bank of America"
}
```

Retrieves a specific bank.

### HTTP Request

`GET ...api/v1/banks/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the bank to retrieve
