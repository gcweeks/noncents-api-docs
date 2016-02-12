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
  "fname": "Cash",
  "lname": "Money",
  "number": "+15555552016",
  "dob": "1990-01-01",
  "created_at": "2016-01-01T01:02:03.004Z",
  "updated_at": "2016-01-02T01:02:03.004Z",
  "email": "cashmoney@gmail.com",
  "invest_percent": 10
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
  "number": "+15555552016",
  "dob": "1990-01-01",
  "created_at": "2016-01-01T01:02:03.004Z",
  "updated_at": "2016-01-02T01:02:03.004Z",
  "email": "cashmoney@gmail.com",
  "invest_percent": 10
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
