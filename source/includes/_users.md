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
  "vices": [],
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
  "invest_percent": 10,
  "vices": [
    "Nightlife",
    "Travel"
  ]
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
  "invest_percent": 10,
  "vices": [
    "Nightlife",
    "Travel"
  ]
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

## Set User Vices

```shell
curl "...api/v1/users/me/vices"
  -d "vices[]=Travel&vices[]=Nightlife"
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
  "invest_percent": 10,
  "vices": [
    "Nightlife",
    "Travel"
  ]
}
```

> Validation errors

```json
{
  "vices":[
    "are nil",
    "are in incorrect format",
    "have one or more invalid names"
  ]
}
```

Sets the authenticated User's Vices. The list of available Vices is given below, and can optionally be obtained by making a call to `GET ...api/v1/vices`. It is worth noting that this call will overwrite the User's existing Vices, so if the goal is to add one Vice, you must first obtain the original list of Vices and then send the augmented list of Vices as a payload to this endpoint. To clear all Vices, simply pass in a Vice of 'None'.

### List of Vices

* `Nightlife`
* `Restaurants`
* `Shopping`
* `FastFood`
* `CoffeeShops`
* `Travel`
* `Experiences`
* `Electronics`
* `PersonalCare`
* `Movies`
* `RideSharing`
* `None` - Will clear all vices

### HTTP Request

`POST ...api/v1/users/me/vices`

### URL Parameters

Parameter | Validations | Description
--------- | ------- | -----------
vices[] | Equal to any of the Vices from the list above | The list of Vices to set for the User

## Plaid

```shell
curl -X GET "...api/v1/users/me/account_auth"
  -d "username=plaid_test&password=plaid_good&type=wells"
  -H "Authorization: TOKEN"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id":1,
    "user_id":1,
    "created_at":"2016-02-19T11:25:18.179-08:00",
    "updated_at":"2016-02-19T11:25:18.179-08:00",
    "plaid_id":"QPO8Jo8vdDHMepg41PBwckXm4KdK1yUdmXOwK",
    "name":"Plaid Savings",
    "institution":"fake_institution",
    "available_balance":null,
    "current_balance":null,
    "account_num":9900009606,
    "routing_num":21000021,
    "account_type":"depository",
    "account_subtype":"savings"
    },
    {
      "..."
    },
    "..."
]
```

> If the account requires MFA, you will instead get a response like this:

```json
{
  "access_token": "test_citi"
}
```

> Validation errors

```json
{
  "username":[
    "is required"
  ],
  "password":[
    "is required"
  ],
  "type":[
    "is required"
  ]
}
```

> Plaid errors

```json
{
  "code": 1200,
  "message": "invalid credentials",
  "resolve": "The username or password provided were not correct."
}
```

Gets all accounts associated with bank credentials and stores them in the User model and returns them to the client. This call is expected to be followed by a call to remove unnecessary accounts, `POST .../api/v1/users/me/remove_accounts`. Otherwise, it will be assumed that the User wants to use all accounts associated with their credentials.

### List of Bank Types

Type | MFA | Third
amex | | Third
bofa | Question-based MFA (3 questions) or code-based MFA (SafePass) | Third
capone360 | Question-based MFA (1 to 3 questions) | Third
schwab | | Third
chase | Code-based MFA | Third
citi | Question-based MFA and selection-based MFA | Third
fidelity | | Third
nfcu | | Third
pnc | Question-based MFA (3 questions) | Third
suntrust | | Third
td | Question-based MFA (1 to 3 questions) | Third
us | Question-based MFA (1 to 3 questions) | Third
usaa | Question-based MFA (3 questions) | Third
wells | | Third

### HTTP Request

`PUT ...api/v1/users/me/account_auth`

### URL Parameters

Parameter | Validations | Description
--------- | ------- | -----------
type | Present | The bank name
username | Present | The bank username
password | Present | The bank password
