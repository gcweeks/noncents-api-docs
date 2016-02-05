# Users

## Get Authenticated User

```shell
curl "...api/v1/users/me"
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
  "created_at": "2016-01-01T01:00:00.000Z",
  "updated_at": "2016-01-02T01:00:00.000Z"
}
```

Retrieves the authenticated User

### HTTP Request

`GET ...api/v1/users/me`

## Update Authenticated User

```shell
curl -X PUT "...api/v1/users/me"
  -d "user[fname]=New&user[lname]=Name"
  -H "Authorization: TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "fname": "New",
  "lname": "Name",
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
  "created_at": "2016-01-01T01:00:00.000Z",
  "updated_at": "2016-01-02T01:00:00.000Z"
}
```

Updates certain fields of the authenticated User

### HTTP Request

`PUT ...api/v1/users/me`

### URL Parameters

Parameter | Required | Description
--------- | ------- | -----------
user[fname] | false | The User's first name
user[lname] | false | The User's last name
