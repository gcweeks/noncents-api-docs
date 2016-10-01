# Authentication

The Noncents API uses API keys to allow access to the API. To acquire an API key, you will need to verify your authenticity by sending an email and password to the server at `/auth`. If successful, the server will return a JSON User model containing a token that will allow for further API authentication. Look at the bar on the right for more information.

The API expects for the auth token to be included in authenticated API requests to the server. You should include this in a header that looks like the following:

`Authorization: TOKEN`

<aside class="notice">
You must replace <code>TOKEN</code> with your personal API key.
</aside>

## Get Token

```shell
curl -X GET "...v1/auth?
  user[email]=cashmoney%40gmail.com&
  user[password]=Ca5hM0n3y"
```

> Successful response:

```json
{
  "id":"7d966671-e36e-5f42-8ed4-fb56cf2f2768",
  "fname":"Cash",
  "lname":"Money",
  "email":"cashmoney@gmail.com",
  "dob":"1990-01-20",
  "invest_percent":10,
  "transactions_refreshed_at":"2016-02-19T11:24:33.873-08:00",
  "goal":420,
  "phone":"5555552016",
  "created_at":"2016-02-19T11:24:33.873-08:00",
  "updated_at":"2016-02-19T11:24:33.873-08:00",
  "dwolla_status":"verified",
  "accounts":["..."],
  "address":"...",
  "agexes":["..."],
  "deposit_account":"...",
  "fund":"...",
  "source_account":"...",
  "transactions":["..."],
  "vices":["..."],
  "yearly_funds":["..."],
  "token":"GPFrZEfm4isNwvqPziJkqj3d"
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

`GET ...v1/auth`

### Query Parameters

Parameter | Validations | Description
--------- | ------- | -----------
user[email] | Present | The User's email.
user[password] | Present, correct | The User's password

## Request Password Reset

```shell
curl -X POST "...v1/reset_password"
  -d "user[email]=cashmoney%40gmail.com"
```

> Validation errors

```json
{
  "email":[
    "can't be blank"
  ]
}
```

Generates a password reset token and sends it in an email to the email address given. The user then has 10 minutes to enter that token and reset their password, which is accomplished using the `PUT ...v1/update_password` route.

### HTTP Request

`POST ...v1/reset_password`

### Query Parameters

Parameter | Validations | Description
--------- | ------- | -----------
user[email] | Present | The User's email.

## Update Password

```shell
curl -X PUT "...v1/update_password"
  -d "token=19knZR&
  user[email]=cashmoney%40gmail.com&
  user[password]=NewPa55word"
```

> Validation errors

```json
{
  "token":[
    "is required",
    "is incorrect",
    "is expired",
    "has never been requested"
  ],
  "email":[
    "is required"
  ],
  "password":[
    "is required",
    "is invalid"
  ]
}
```

Allows a user with a password reset token to reset their account password. The reset token is sent to the user via email, and they have 10 minutes from the time it was requested with `POST ...v1/reset_password` to use the token before it expires. This route requires the email of the user as well as the new password, which must obey the standard password validation constraints.

### HTTP Request

`PUT ...v1/update_password`

### Query Parameters

Parameter | Validations | Description
--------- | ------- | -----------
token | Present | The password reset token
user[email] | Present | The User's email.
user[password] | Minimum 8 characters, 1 uppercase letter, 1 lowercase letter, 1 number | The User's new password
