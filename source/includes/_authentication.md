# Authentication

The Dimention API uses API keys to allow access to the API. To acquire an API key, you will need to verify your authenticity by requesting an SMS confirmation code at `/confirmation`. Once the client obtains this code via SMS, it will need to be send to `/auth`. If successful, the server will return a JSON User model containing a token that will allow for further API authentication. Look at the bar on the right for more information.

The API expects for the auth token to be included in authenticated API requests to the server. You should include this in a header that looks like the following:

`Authorization: TOKEN`

<aside class="notice">
You must replace <code>TOKEN</code> with your personal API key.
</aside>

## Sign Up

```shell
curl "...api/v1/signup"
  -d "user[fname]=Cash&
  user[lname]=Money&
  user[email]=cashmoney%40gmail.com
  user[password]=Ca5hM0n3y
  user[dob]=1990-01-01
  user[number]=%2b15555552016"
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
  "token": "GPFrZEfm4isNwvqPziJkqj3d"
}
```

> Validation errors

```json
{
  "fname":[
    "can't be blank"
  ],
  "lname":[
    "can't be blank"
  ],
  "email":[
    "can't be blank",
    "is invalid",
    "has already been taken"
  ],
  "password":[
    "can't be blank",
    "is too short (minimum is 8 characters)"
  ],
  "dob":[
    "can't be blank"
  ],
}
```

Creates a new User. Accepts an email, a first name, and a last name, date of birth, and optionally a phone number. If successful, this call returns the created User model in addition to that user's token. If one of the required fields is absent, the email has already been taken, the email has an invalid format, or the password is less than 8 characters, a validation error will be returned with the error code "422 Unprocessable Entity"

### HTTP Request

`POST ...api/v1/signup`

### Query Parameters

Parameter | Validations | Description
--------- | ------- | -----------
user[fname] | Present | The User's first name
user[lname] | Present | The User's last name
user[email] | Present, email-format, unique | The User's email.
user[password] | Minimum 8 characters | The User's password
user[dob] | Present | The User's date of birth
user[number] | None | The User's phone number

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
