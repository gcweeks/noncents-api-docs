# Banks

## Get a Specific Bank

```shell
curl -X GET "...api/v1/banks/3"
  -H "Authorization: TOKEN"
```

> Successful response:

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
