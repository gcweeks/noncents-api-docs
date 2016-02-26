# Users

## Sign Up

```shell
curl -X POST "...api/v1/users"
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
curl -X GET "...api/v1/users/me"
  -H "Authorization: TOKEN"
```

> Successful response:

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

> Successful response:

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
curl -X PUT "...api/v1/users/me/vices"
  -d "vices[]=Travel&vices[]=Nightlife"
  -H "Authorization: TOKEN"
```

> Successful response:

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

## Plaid Connect

```shell
curl -X GET "...api/v1/users/me/account_connect"
  -d "username=cashmoney&password=Ca5hM0ney&type=wells"
  -H "Authorization: TOKEN"
```

> Successful response:
> (Note that the "accounts" array will be populated with a list of all accounts at the given bank. To remove unneeded accounts, use users/me/remove_accounts)

```json
{
  "id": 1,
  "fname": "Cash",
  "lname": "Money",
  "number": "+15555552016",
  "created_at": "2016-02-19T11:24:33.873-08:00",
  "updated_at": "2016-02-19T11:24:33.873-08:00",
  "email": "cashmoney@gmail.com",
  "dob": "1990-01-20",
  "invest_percent": 10,
  "accounts": [
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
    "..."
  ],
  "vices": []
}
```

> If the account requires MFA, you will instead get a response like this:

```json
{
  "accounts":[],
  "transactions":[],
  "permissions":["connect"],
  "access_token":"test_9b97b...265ac",
  "api_res":"Requires further authentication",
  "info":{},
  "pending_mfa_questions":
  {
    "type":"device",
    "mfa":
    {
      "message":"Code sent to c...y@gmail.com"
    },
    "access_token":"9b97b...265ac"
  }
}
```

> The following are a list of pending_mfa_questions styles you will encounter:

```json
{
  "type":"questions",
  "mfa":[
    {
      "question":"You say tomato, I say...?"
    }
  ],
  "access_token":"9b97b...265ac"
}

{
  "type":"device",
  "mfa":
  {
    "message":"Code sent to t...t@plaid.com"
  },
  "access_token":"9b97b...265ac"
}

{
  "type":"selections",
  "mfa":[
    {
      "question":"You say tomato, I say...?",
      "answers":["tomato","potato"]
    },
    {
      "question":"Ketchup or mustard?",
      "answers":["ketchup","mustard"]
    }
  ],
  "access_token": "9b97b...265ac"
}
```

> You will need to submit a GET request to the users/me/account_mfa route

```json
```

> If the bank requires a code that they sent to the user's email/phone (chase/bofa), you will instead be given a list of devices so the user can select which device they want the code sent to

```json
{
  "type": "list",
  "mfa": [
    {
      "mask": "xxx-xxx-5309",
      "type": "phone"
    },
    {
      "mask": "t..t@plaid.com",
      "type": "email"
    }
  ],
  "access_token": "9b97b...265ac"
}
```

> You can then use this information to send the proper call to the users/me/account_mfa route

```json
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

> Plaid errors (there are a variety but these are a few I've come across)

```json
{
  "code": 1200,
  "message": "invalid credentials",
  "resolve": "The username or password provided were not correct."
}

{
  "code": 1215,
  "message": "mfa reset",
  "resolve": "MFA access has changed or this application's access has been revoked. Submit a PATCH call to resolve."
}

{
  "code": 1003,
  "message": "access_token disallowed",
  "resolve": "You included an access_token on a submit call - this is only allowed on step and get routes."
}
```

Gets all accounts associated with bank credentials and stores them in the User model and returns them to the client. This call is expected to be followed by a call to remove unnecessary accounts, `POST .../api/v1/users/me/remove_accounts`. Otherwise, it will be assumed that the User wants to use all accounts associated with their credentials.

### List of Bank Types

Type | PIN | MFA
---- | --- | ---
amex | No | None
bofa | No | Question-based MFA (3 questions) or code-based MFA (SafePass)
capone360 | No | Question-based MFA (1 to 3 questions)
schwab | No | None
chase | No | Code-based MFA
citi | No | Question-based MFA and selection-based MFA
fidelity | No | None
nfcu | No | None
pnc | No | Question-based MFA (3 questions)
suntrust | No | None
td | No | Question-based MFA (1 to 3 questions)
us | No | Question-based MFA (1 to 3 questions)
usaa | Yes | Question-based MFA (3 questions)
wells | No | None

### HTTP Request

`GET ...api/v1/users/me/account_connect`

### URL Parameters

Parameter | Validations | Description
--------- | ------- | -----------
type | Present | The bank name
username | Present | The bank username
password | Present | The bank password

## Plaid MFA

```shell
curl -X GET "...api/v1/users/me/account_mfa"
  -d "access_token=9b97b...265ac&answer=12345687"
  -H "Authorization: TOKEN"
```

> The JSON response and errors here are identical to those of users/me/account_connect. To see a list of everything that can be returned, visit the users/me/account_connect section of the API documentation

```json
```

> Validation errors

```json
{
  "answer":[
    "is required (unless selecting MFA method)"
  ],
  "mask":[
    "can be submitted instead of answer to select MFA method"
  ],
  "type":[
    "can be submitted instead of answer to select MFA method"
  ]
}
```

If a call `GET .../api/v1/users/me/account_connect` requires Multi-Factor Authentication (MFA), you will instead have to use this route to successfully connect with the user's bank accounts.

To submit an answer to an MFA question or code, use the `answer` field.

To specify which particular device you would like to receive your code (if doing code-based MFA, i.e. bofa/chase), use the `mask` or `type` fields. The `type` field lets you specify the device type, i.e. "phone" or "email". `mask` lets you get more specific. For example, if the user has multiple phones, you can specify the correct phone number by using `mask=xxx-xxx-5309` in your call. To get a better idea of your options, make sure you've read the returned JSON list of device options in the account_connect section of the API documentation.

### HTTP Request

`GET ...api/v1/users/me/account_mfa`

### URL Parameters

Parameter | Validations | Description
--------- | ------- | -----------
answer | Present unless 'mask' or 'type' are present | Answer to the MFA
mask | Present unless 'answer' or 'type' are present | MFA device selection based on device mask
type | Present unless 'mask' or 'answer' are present | The bank password

## Remove Accounts

```shell
curl -X PUT "...api/v1/users/me/remove_accounts"
  -d "accounts[]=1234&accounts[]=5678"
  -H "Authorization: TOKEN"
```

> Successful response:

```json
{
  "id":1,
  "fname":"Cash",
  "lname":"Money",
  "number":"+15555552016",
  "created_at":"2016-02-19T11:24:33.873-08:00",
  "updated_at":"2016-02-19T11:24:33.873-08:00",
  "email":"cashmoney@gmail.com",
  "dob":"1990-01-20",
  "invest_percent":10,
  "accounts":[
    {
      "id":6,
      "user_id":1,
      "created_at":"2016-02-19T11:40:35.232-08:00",
      "updated_at":"2016-02-25T15:36:25.588-08:00",
      "plaid_id":"nban4wnPKEtnmEpaKzbYFYQvA7D7pnCaeDBMy",
      "name":"Plaid Checking",
      "institution":"fake_institution",
      "available_balance":null,
      "current_balance":null,
      "account_num":0,
      "routing_num":0,
      "account_type":"depository",
      "account_subtype":"checking"
    },
    "..."
  ],
  "vices":[]
}
```

> Validation errors

```json
{
  "accounts":[
    "are required",
    "are in incorrect format"
  ]
}
```

After acquiring all of the user's bank accounts, they may not want to track them all. For instance, they may want to track spending from a checking account, but not from a savings account at the same bank. This endpoint lets the user select only the accounts they want to keep and discard the rest.

To specify which accounts to remove, pass in an array `accounts` that contains the ID of each account you want to remove.

### HTTP Request

`PUT ...api/v1/users/me/remove_accounts`

### URL Parameters

Parameter | Validations | Description
--------- | ------- | -----------
accounts[] | Required | An array of Account IDs for Accounts you wish to delete
