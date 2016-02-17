# Users

## Sign Up

```shell
curl "...api/v1/users"
  -d "user[fname]=Cash&
  user[lname]=Money&
  user[email]=cashmoney%40gmail.com&
  user[password]=Ca5hM0n3y&
  user[dob]=1990-01-20&
  user[invest_percent]=10&
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
  "invest_percent": 10,
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
  ]
}
```

Creates a new User. Accepts an email, a first name, and a last name, date of birth, and optionally a phone number. If successful, this call returns the created User model in addition to that user's token. If one of the required fields is absent, the email has already been taken, the email has an invalid format, the invest_percent is not between 0 and 100, or the password is less than 8 characters, a validation error will be returned with the error code "422 Unprocessable Entity"

### HTTP Request

`POST ...api/v1/users`

### Query Parameters

Parameter | Validations | Description
--------- | ------- | -----------
user[fname] | Present | The User's first name
user[lname] | Present | The User's last name
user[email] | Present, email-format, unique | The User's email.
user[password] | Minimum 8 characters | The User's password
user[dob] | Present | The User's date of birth
user[invest_percent] | Between 0 and 100 (Default 0) | The User's spend-to-save percentage
user[number] | None | The User's phone number

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

> Validation errors

```json
{
  "fname":[
    "can't be blank"
  ],
  "lname":[
    "can't be blank"
  ],
  "password":[
    "can't be blank",
    "is too short (minimum is 8 characters)"
  ],
  "dob":[
    "can't be blank"
  ]
}
```

Updates certain fields of the authenticated User. Validations only apply to fields send to the server for update. All other fields will remain the same.

### HTTP Request

`PUT ...api/v1/users/me`

### URL Parameters

Parameter | Validations | Description
--------- | ------- | -----------
user[fname] | Present | The User's first name
user[lname] | Present | The User's last name
user[password] | Minimum 8 characters | The User's password
user[invest_percent] | Between 0 and 100 (Default 0) | The User's spend-to-save percentage
user[number] | None | The User's phone number
