# Authentication

The Dimention API uses API keys to allow access to the API. To acquire an API key, you will need to verify your authenticity by sending an email and password to the server at `/auth`. If successful, the server will return a JSON User model containing a token that will allow for further API authentication. Look at the bar on the right for more information.

The API expects for the auth token to be included in authenticated API requests to the server. You should include this in a header that looks like the following:

`Authorization: TOKEN`

<aside class="notice">
You must replace <code>TOKEN</code> with your personal API key.
</aside>

## Get Token

```shell
curl -X GET "...api/v1/auth?
  user[email]=cashmoney%40gmail.com&
  user[password]=Ca5hM0n3y"
```

> Successful response:

```json
{
  "id": 2,
  "fname": "Cash",
  "lname": "Money",
  "number": "+15555552016",
  "created_at": "2016-01-01T01:02:03.004Z",
  "updated_at": "2016-01-02T01:02:03.004Z",
  "email": "cashmoney@gmail.com",
  "dob": "2000-01-01",
  "invest_percent": 10,
  "token": "GPFrZEfm4isNwvqPziJkqj3d"
}
```

> Validation errors

```json
{
  "email":[
    "can't be blank"
  ],
  "password":[
    "can't be blank",
    "is incorrect"
  ]
}
```

Accepts an email and password and, if successful, returns the User model (containing that User's token) corresponding to the given email.

### HTTP Request

`GET ...api/v1/auth`

### Query Parameters

Parameter | Validations | Description
--------- | ------- | -----------
user[email] | Present | The User's email.
user[password] | Present, correct | The User's password