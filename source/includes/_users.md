# Users

## Get a Specific User

```shell
curl "...api/v1/users/2"
  -H "Authorization: TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "fname": "Ethan",
  "lname": "Held",
  "number": "+18001234567",
  "address": "123 Some St.",
  "city": "Los Angeles",
  "state": "CA",
  "zip": "90000",
  "dob": "1990-01-01",
  "accounts":
  [
    "1234",
    "5678"
  ],
  "token": "abc123..."
}
```

Retrieves a specific user.

### HTTP Request

`GET ...api/v1/users/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the user to retrieve
