# Users

## Check Email

```shell
curl -X GET "...api/v1/check_email"
  -d "email=cashmoney@gmail.com"
  -H "Authorization: TOKEN"
```

> Possible Responses:

```json
{
  "email":"exists",
  "email":"does not exist"
}
```

Check to see if a User exists with the given email

### HTTP Request

`GET ...api/v1/check_email`

### Query Parameters

Parameter | Validations | Description
--------- | ----------- | -----------
email | Present | The User's email

## Sign Up

```shell
curl -X POST "...api/v1/users"
  -d "user[fname]=Cash&
  user[lname]=Money&
  user[email]=cashmoney%40gmail.com&
  user[password]=Ca5hM0n3y&
  user[dob]=1990-01-20&
  user[invest_percent]=10&
  user[goal]=420"
  user[phone]=5555552016&
```

> Successful response:

```json
{
  "id":"7d966671-e36e-5f42-8ed4-fb56cf2f2768",
  "fname":"Cash",
  "lname":"Money",
  "created_at":"2016-02-19T11:24:33.873-08:00",
  "updated_at":"2016-02-19T11:24:33.873-08:00",
  "email":"cashmoney@gmail.com",
  "dob":"1990-01-20",
  "invest_percent":10,
  "sync_date":"2016-02-19T11:24:33.873-08:00",
  "goal":420,
  "phone":"5555552016",
  "fund":{
    "id":"9bf406fc-cc64-45e2-b536-df9f1b0caa4a",
    "balance":"0.0",
    "user_id":"7d966671-e36e-5f42-8ed4-fb56cf2f2768",
    "created_at":"2016-02-19T11:24:33.873-08:00",
    "updated_at":"2016-02-19T11:24:33.873-08:00",
    "amount_invested":"0.0"
  },
  "accounts":[],
  "agexes":[],
  "transactions":[],
  "vices":[],
  "yearly_funds":[],
  "token":"GPFrZEfm4isNwvqPziJkqj3d"
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
    "is invalid"
  ],
  "dob":[
    "can't be blank"
  ],
  "invest_percent":[
    "is not included in the list"
  ],
  "goal":[
    "is not included in the list"
  ],
  "phone":[
    "is invalid"
  ]
}
```

Creates a new User. Accepts an email, a first name, and a last name, date of birth, and optionally a phone number. If successful, this call returns the created User model in addition to that user's token. If one of the required fields is absent, the email has already been taken, the email has an invalid format, the invest_percent is not between 0 and 100, or the password is less than 8 characters, a validation error will be returned with the error code "422 Unprocessable Entity"

<aside class="notice">
When the server returns a User whose Address has not been set, the JSON will not include an 'address' key.
</aside>

### HTTP Request

`POST ...api/v1/users`

### Query Parameters

Parameter | Validations | Description
--------- | ----------- | -----------
user[fname] | Present | The User's first name
user[lname] | Present | The User's last name
user[email] | Present, email-format, unique | The User's email.
user[password] | Minimum 8 characters, 1 uppercase letter, 1 lowercase letter, 1 number | The User's password
user[dob] | Present | The User's date of birth
user[invest_percent] | Between 0 and 100 (Default 0) | The User's spend-to-save percentage
user[goal] | Between 1 and 5500 (Default 230) | The User's monthly investment goal
user[phone] | 10 digits | The User's phone number

## Get Authenticated User

```shell
curl -X GET "...api/v1/users/me"
  -H "Authorization: TOKEN"
```

> Successful response:

```json
{
  "id":"7d966671-e36e-5f42-8ed4-fb56cf2f2768",
  "fname":"Cash",
  "lname":"Money",
  "created_at":"2016-02-19T11:24:33.873-08:00",
  "updated_at":"2016-02-19T11:24:33.873-08:00",
  "email":"cashmoney@gmail.com",
  "dob":"1990-01-20",
  "invest_percent":10,
  "sync_date":"2016-02-19T11:24:33.873-08:00",
  "goal":420,
  "phone":"5555552016",
  "fund":"...",
  "address":"...",
  "accounts":["..."],
  "agexes":["..."],
  "transactions":["..."],
  "vices":["..."],
  "yearly_funds":["..."]
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
  "id":"7d966671-e36e-5f42-8ed4-fb56cf2f2768",
  "fname":"New",
  "lname":"Name",
  "fname":"Cash",
  "lname":"Money",
  "created_at":"2016-02-19T11:24:33.873-08:00",
  "updated_at":"2016-02-19T11:24:33.873-08:00",
  "email":"cashmoney@gmail.com",
  "dob":"1990-01-20",
  "invest_percent":10,
  "sync_date":"2016-02-19T11:24:33.873-08:00",
  "goal":420,
  "phone":"5555552016",
  "fund":"...",
  "address":"...",
  "accounts":["..."],
  "agexes":["..."],
  "transactions":["..."],
  "vices":["..."],
  "yearly_funds":["..."]
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
  "invest_percent":[
    "is not included in the list"
  ],
  "goal":[
    "is not included in the list"
  ],
  "phone":[
    "is invalid"
  ]
}
```

Updates certain fields of the authenticated User. Validations only apply to fields sent to the server for update. All other fields will remain the same. Some fields, such as email and date of birth, cannot be changed. See the provided "URL Parameters" table to see which fields can be modified.

### HTTP Request

`PUT ...api/v1/users/me`

### URL Parameters

Parameter | Validations | Description
--------- | ----------- | -----------
user[fname] | Present | The User's first name
user[lname] | Present | The User's last name
user[password] | Minimum 8 characters, 1 uppercase letter, 1 lowercase letter, 1 number | The User's password
user[invest_percent] | Between 0 and 100 (Default 0) | The User's spend-to-save percentage
user[goal] | Between 1 and 5500 (Default 230) | The User's monthly investment goal
user[phone] | 10 digits | The User's phone number

## Get Current YearlyFund

```shell
curl -X GET "...api/v1/users/me/yearly_fund"
  -H "Authorization: TOKEN"
```

> Successful response:

```json
{
  "id":"7d966671-e36e-5f42-8ed4-fb56cf2f2768",
  "balance":"1.53",
  "amount_invested":"0.53",
  "year":2016,
  "user_id":"7d966671-e36e-5f42-8ed4-fb56cf2f2768",
  "created_at":"2016-02-19T11:24:33.873-08:00",
  "updated_at":"2016-02-19T11:24:33.873-08:00"
}
```

A YearlyFund model is just like a Fund model, except limited to only the
deposits (and interest) for a given tax year. This method grabs the user's
current YearlyFund model (that is, the YearlyFund model associated with the
current tax year). If no YearlyFund model exists for the current tax year, one
will be created as a result of this call.

### HTTP Request

`GET ...api/v1/users/me/yearly_fund`

## Set User Vices

```shell
curl -X PUT "...api/v1/users/me/vices"
  -d "vices[]=Travel&vices[]=Nightlife"
  -H "Authorization: TOKEN"
```

> Successful response:

```json
{
  "id":"7d966671-e36e-5f42-8ed4-fb56cf2f2768",
  "fname":"Cash",
  "lname":"Money",
  "created_at":"2016-02-19T11:24:33.873-08:00",
  "updated_at":"2016-02-19T11:24:33.873-08:00",
  "email":"cashmoney@gmail.com",
  "dob":"1990-01-20",
  "invest_percent":10,
  "sync_date":"2016-02-19T11:24:33.873-08:00",
  "goal":420,
  "phone":"5555552016",
  "fund":"...",
  "address":"...",
  "accounts":["..."],
  "agexes":["..."],
  "transactions":["..."],
  "vices":[
    "Nightlife",
    "Travel"
  ],
  "yearly_funds":["..."]
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
--------- | ----------- | -----------
vices[] | Equal to any of the Vices from the list above | The list of Vices to set for the User

## Set User Address

```shell
curl -X PUT "...api/v1/users/me/address"
  -d "address[line1]=123\ Cashmoney\ Lane&
  address[line2]=Apt\ 420&
  address[city]=Los\ Angeles&
  address[state]=CA&
  address[zip]=90024"
  -H "Authorization: TOKEN"
```

> Successful response:

```json
{
  "id":"7d966671-e36e-5f42-8ed4-fb56cf2f2768",
  "fname":"Cash",
  "lname":"Money",
  "created_at":"2016-02-19T11:24:33.873-08:00",
  "updated_at":"2016-02-19T11:24:33.873-08:00",
  "email":"cashmoney@gmail.com",
  "dob":"1990-01-20",
  "invest_percent":10,
  "sync_date":"2016-02-19T11:24:33.873-08:00",
  "goal":420,
  "phone":"5555552016",
  "fund":"...",
  "address":{
    "id":"9bf406fc-cc64-45e2-b536-df9f1b0caa4a",
    "line1":"123 Cashmoney Lane",
    "line2":"Apt 420",
    "city":"Los Angeles",
    "state":"CA",
    "zip":"90024",
    "user_id":"7d966671-e36e-5f42-8ed4-fb56cf2f2768",
    "created_at":"2016-07-20T16:53:30.027-07:00",
    "updated_at":"2016-07-20T16:53:30.027-07:00"
  },
  "accounts":["..."],
  "agexes":["..."],
  "transactions":["..."],
  "vices":["..."],
  "yearly_funds":["..."]
}
```

> Validation errors

```json
{
  "line1":[
    "can't be blank"
  ],
  "city":[
    "can't be blank"
  ],
  "state":[
    "can't be blank"
  ],
  "zip":[
    "can't be blank"
  ]
}
```

Sets the authenticated User's Address. If the User does not already have an Address, omitting any of the required fields in the request will result in a validation error. If the User already has a full Address stored, however, you may submit a PUT request that only changes a particular field (as long as it does not set a required field to null).

<aside class="notice">
When the server returns a User whose Address has not been set, the JSON will not include an 'address' key.
</aside>

### HTTP Request

`POST ...api/v1/users/me/address`

### URL Parameters

Parameter | Validations | Description
--------- | ----------- | -----------
address[line1] | Present  | The street address
address[line2] | Optional | Second line for street address, for things like apartment numbers
address[city]  | Present  | The city
address[state] | Present  | The state
address[zip]   | Present  | The postal code

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
  "id":"7d966671-e36e-5f42-8ed4-fb56cf2f2768",
  "fname":"Cash",
  "lname":"Money",
  "created_at":"2016-02-19T11:24:33.873-08:00",
  "updated_at":"2016-02-19T11:24:33.873-08:00",
  "email":"cashmoney@gmail.com",
  "dob":"1990-01-20",
  "invest_percent":10,
  "sync_date":"2016-02-19T11:24:33.873-08:00",
  "goal":420,
  "phone":"5555552016",
  "fund":"...",
  "address":"...",
  "accounts":[
    {
      "id":"3dce9e2f-5321-431d-bd67-9ab3db32a4d3",
      "created_at":"2016-02-19T11:25:18.179-08:00",
      "updated_at":"2016-02-19T11:25:18.179-08:00",
      "plaid_id":"QPO8Jo8vdDHMepg41PBwckXm4KdK1yUdmXOwK",
      "name":"Plaid Savings",
      "institution":"fake_institution",
      "available_balance":null,
      "current_balance":null,
      "account_type":"depository",
      "account_subtype":"savings",
      "user_id":"7d966671-e36e-5f42-8ed4-fb56cf2f2768",
      "bank_id":"e780c643-5006-4730-8055-383ae8e97978",
      "tracking":false,
      "dwolla_id":"97ba8ac0-27ef-45d9-a611-d2a4896b8332",
      "account_num":"9900009606",
      "routing_num":"021000021"
    },
    "..."
  ],
  "agexes":["..."],
  "transactions":["..."],
  "vices":["..."],
  "yearly_funds":["..."]
}
```

> If the account requires MFA, you will instead get a response like this:

```json
{
  "access_token":"9b97b...265ac",
  "mfa_type":"questions",
  "mfa":[
    {
      "question":"You say tomato, I say...?"
    }
  ]
}
```

> If the bank requires a code that they sent to the user's email/phone (chase/bofa only), you will instead be given a list of devices so the user can select which device they want the code sent to

```json
{
  "access_token":"9b97b...265ac",
  "mfa_type":"questions",
  "mfa":[
    {
      "mask":"xxx-xxx-2016",
      "type":"phone"
    },
    {
      "mask":"c..y@gmail.com",
      "type":"email"
    }
  ]
}
```

> You can then use this information to send the proper call to the users/me/account_mfa route using the given "mask" or "type" fields

```json
```

> The following are a list of pending_mfa_questions styles you will encounter:

```json
{
  "access_token":"9b97b...265ac",
  "mfa_type":"questions",
  "mfa":[
    {
      "question":"You say tomato, I say...?"
    }
  ]
}

{
  "access_token":"9b97b...265ac",
  "mfa_type":"device",
  "mfa":[
    {
      "message":"Code sent to t...t@plaid.com"
    }
  ]
}

{
  "access_token":"9b97b...265ac",
  "mfa_type":"selections",
  "mfa":[
    {
      "question":"You say tomato, I say...?",
      "answers":["tomato","potato"]
    },
    {
      "question":"Ketchup or mustard?",
      "answers":["ketchup","mustard"]
    }
  ]
}
```

> You will need to submit a GET request to the users/me/account_mfa route

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
  "code":1200,
  "message":"Code 1200: invalid credentials. The username or password provided were not correct.",
  "resolve":"The username or password provided were not correct."
}

{
  "code":1203,
  "message":"Code 1203: invalid mfa. The MFA response provided was not correct.",
  "resolve":"The MFA response provided was not correct."
}
```

Gets all accounts associated with bank credentials and stores them in the User model and returns them to the client. This call is expected to be followed by a call to remove unnecessary accounts, `POST .../api/v1/users/me/remove_accounts`. Otherwise, it will be assumed that the User wants to use all accounts associated with their credentials.

To perform this call, provide a bank type (listed in the table below), username, and password. If the bank type is 'usaa', you must additionally provide a pin.

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
--------- | ----------- | -----------
type | Present | The bank name
username | Present | The bank username
password | Present | The bank password
pin | Optional | The bank pin (usaa only)

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

## Set Accounts

```shell
curl -X PUT "...api/v1/users/me/accounts"
  -d "source=9bf406fc-cc64-45e2-b536-df9f1b0caa4a&
      deposit=3dce9e2f-5321-431d-bd67-9ab3db32a4d3&
      tracking[]=9bf406fc-cc64-45e2-b536-df9f1b0caa4a&
      tracking[]=32ebc551-7365-408c-bad4-c820a44a8860"
  -H "Authorization: TOKEN"
```

> Successful response:

```json
{
  "id":"7d966671-e36e-5f42-8ed4-fb56cf2f2768",
  "fname":"Cash",
  "lname":"Money",
  "created_at":"2016-02-19T11:24:33.873-08:00",
  "updated_at":"2016-02-19T11:24:33.873-08:00",
  "email":"cashmoney@gmail.com",
  "dob":"1990-01-20",
  "invest_percent":10,
  "sync_date":"2016-02-19T11:24:33.873-08:00",
  "goal":420,
  "source_account_id":"9bf406fc-cc64-45e2-b536-df9f1b0caa4a",
  "deposit_account_id":"32ebc551-7365-408c-bad4-c820a44a8860",
  "phone":"5555552016",
  "fund":"...",
  "address":"...",
  "accounts":["..."],
  "agexes":["..."],
  "transactions":["..."],
  "vices":["..."],
  "yearly_funds":["..."]
}
```

> Validation errors

```json
{
  "general":[
    "Missing parameter. Options are one or more of: \"source\", \"deposit\", \"tracking\""
  ],
  "source":[
    "Account not found",
    "is incorrectly formatted - must be of type String"
  ],
  "deposit":[
    "Account not found",
    "is incorrectly formatted - must be of type String"
  ],
  "tracking":[
    "Account not found",
    "is incorrectly formatted - must be of type Array"
  ]
}
```

After acquiring all of the user's bank accounts, they need to specify which Accounts they want to track and which they want to use for deduction. For instance, they may want to track spending from a checking account, but not from a savings account at the same bank, and they may want to deduct from their checking account into their savings account every week.

To specify which Accounts to track, pass in an array `tracking[]` that contains the ID of each Account you want to track. To specify an Account to deduct money into each week, pass in the key `deposit` with the ID of the Account as its value. Similarly, for the Account to deduct money from, use the `source` key.

You may use this route do set multiple Accounts at once. For example, you can track multiple Accounts and add the source/deposit Accounts all in one call. This route is also idempotent, meaning that adding Accounts as source/deposit/tracking multiple times will not have any adverse effects. Similarly, passing in a new source/deposit Account will override the previous ones. Passing in a new tracking Account will add it to the array of Accounts to track. If instead you wish to remove a tracking Account, use the `DELETE` REST call for this same route. For more information on deleting Accounts, see the relevant section in the documentation.

### HTTP Request

`PUT ...api/v1/users/me/accounts`

### URL Parameters

Parameter | Validations | Description
--------- | ----------- | -----------
source | String | ID of Account to deduct money from
deposit | String | ID of Account to deposit money into
accounts[] | Array | IDs for Accounts you wish to track

## Remove Accounts

```shell
curl -X DELETE "...api/v1/users/me/accounts"
  -d "source=anything&
      deposit=anything&
      tracking[]=9bf406fc-cc64-45e2-b536-df9f1b0caa4a&
      tracking[]=32ebc551-7365-408c-bad4-c820a44a8860"
  -H "Authorization: TOKEN"
```

> Successful response:

```json
{
  "id":"7d966671-e36e-5f42-8ed4-fb56cf2f2768",
  "fname":"Cash",
  "lname":"Money",
  "created_at":"2016-02-19T11:24:33.873-08:00",
  "updated_at":"2016-02-19T11:24:33.873-08:00",
  "email":"cashmoney@gmail.com",
  "dob":"1990-01-20",
  "invest_percent":10,
  "sync_date":"2016-02-19T11:24:33.873-08:00",
  "goal":420,
  "phone":"5555552016",
  "source_account_id":null,
  "deposit_account_id":null,
  "fund":"...",
  "address":"...",
  "accounts":["..."],
  "agexes":["..."],
  "transactions":["..."],
  "vices":["..."],
  "yearly_funds":["..."]
}
```

> Validation errors

```json
{
  "general":[
    "Missing parameter. Options are one or more of: \"source\", \"deposit\", \"tracking\""
  ],
  "tracking":[
    "Account not found",
    "is incorrectly formatted - must be of type Array"
  ]
}
```

Use this route to stop tracking the spending on certain Accounts, or to remove a weekly deduction source or deposit account (keep in mind this will prevent the User from being able to save money).

To specify which Accounts to stop tracking, pass in an array `tracking[]` that contains the ID of each Account you want to stop tracking. To remove a deduction or source Account, pass in the key `deposit` or `source`, respectively, with any value (the value is ignored).

You may use this route do remove multiple Accounts at once. For example, you can stop tracking multiple Accounts and remove the source/deposit Accounts all in one call. This route is also idempotent, meaning that removing Accounts as source/deposit/tracking multiple times will not have any adverse effects.

### HTTP Request

`DELETE ...api/v1/users/me/accounts`

### URL Parameters

Parameter | Validations | Description
--------- | ----------- | -----------
source | None | Remove the User's source Account
deposit | None | Remove the User's deposit Account
accounts[] | Array | IDs for Accounts you wish to stop tracking

## Refresh Transactions

```shell
curl -X POST "...api/v1/users/me/refresh_transactions"
  -H "Authorization: TOKEN"
```

> Successful response:

```json
{
  "id":"7d966671-e36e-5f42-8ed4-fb56cf2f2768",
  "fname":"Cash",
  "lname":"Money",
  "created_at":"2016-02-19T11:24:33.873-08:00",
  "updated_at":"2016-02-19T11:24:33.873-08:00",
  "email":"cashmoney@gmail.com",
  "dob":"1990-01-20",
  "invest_percent":10,
  "sync_date":"2016-02-19T11:24:33.873-08:00",
  "goal":420,
  "phone":"5555552016",
  "fund":"...",
  "address":"...",
  "accounts":["..."],
  "agexes":["..."],
  "transactions":[
    {
      "id":"9bf406fc-cc64-45e2-b536-df9f1b0caa4a",
      "plaid_id":"KdDjmojBERUKx3JkDdO5IaRJdZeZKNuK4bnKJ1",
      "date":"2014-06-23",
      "amount":"2307.15",
      "name":"Apple Store",
      "category_id":"19013000",
      "account_id":"3dce9e2f-5321-431d-bd67-9ab3db32a4d3",
      "created_at":"2016-02-19T11:24:33.873-08:00",
      "updated_at":"2016-02-19T11:24:33.873-08:00",
      "user_id":"7d966671-e36e-5f42-8ed4-fb56cf2f2768",
      "invested":false,
      "backed_out":true,
      "amount_invested":"0.0",
      "vice":"Electronics"
    },
    "..."
  ],
  "vices":["..."],
  "yearly_funds":["..."]
}
```

This route pulls the user's latest transactions. Transactions are pulled for every bank they have authenticated with, then filtered down to only the accounts they have selected (see "Remove Accounts"), then further filtered down to only the transactions that correspond to vices the user has selected (see "Set User Vices") and finally stored in the user model (User.transactions). The entire user model is returned as a result of this call.

### HTTP Request

`POST ...api/v1/users/me/refresh_transactions`

## Register for FCM Notifications

```shell
curl -X POST "...api/v1/users/me/register_push_token"
  -d "token=1234..."
  -H "Authorization: TOKEN"
```

> Possible Responses:

```json
{
  "status":"registered",
  "status":"failed to register"
}
```

> Validation errors

```json
{
  "token":[
    "is required"
  ]
}
```

Use this route to register for FCM push notifications. FCM uses the concept of "Groups" to organize each of the devices associated with a given user. In this way, rather than sending a notification to a particular device, a notification is sent to all devices that are associated with that User ID. This avoids issues with sending notifications to the user when they have multiple devices or have uninstalled the app and reinstalled it on a new device.

To associate a given device with an FCM Group, you must obtain an FCM device registration token and POST it to this route. Then, any notification for your user will be sent to the `user_<User.id>` FCM Group, which will contain all of the device registration tokens you have POSTed to this route as that User, sending push notifications the corresponding devices.

### HTTP Request

`POST ...api/v1/users/me/register_push_token`

## Create Dwolla Customer

```shell
curl -X POST "...api/v1/users/me/dwolla"
  -d "ssn=123-45-6789&address[line1]=..."
  -H "Authorization: TOKEN"
```

> Validation errors

```json
{
  "ssn":[
    "is required"
  ],
  "address":[
    "is required"
  ]
}
```

Use this route to create a Dwolla Customer object for the authed User. A Dwolla Customer is required to perform any transactions between accounts, as a Dwolla Funding Source (bank account) needs to be attached to an existing Dwolla Customer. Because we use Plaid, Dwolla funding sources are automatically verified. However, this is not true for Customers, which need to be verified using a physical address, SSN, and IP address. The IP address is determined based on the IP address that made the server call, but the SSN and physical address must be passed in as parameters to this endpoint. One exception is that if the authenticated User already has a stored Address, that address will be used if the `address` parameter is missing from the payload. If the `address` parameter is present regardless, that information will be used to update the User's stored Address.

Note that while the SSN is passed in as `ssn`, an address field is passed in as `address[line1]`, etc. Also note that while the address is saved on the server, the SSN is merely passed to Dwolla and forgotten at the end of the server call.

### HTTP Request

`POST ...api/v1/users/me/dwolla`

### URL Parameters

Parameter | Validations | Description
--------- | ----------- | -----------
ssn | Present  | Social security number
address[line1] | Present  | The street address
address[line2] | Optional | Second line for street address, for things like apartment numbers
address[city]  | Present  | The city
address[state] | Present  | The state
address[zip]   | Present  | The postal code

## Send Slack Support Ticket

```shell
curl -X POST "...api/v1/users/me/support"
  -d "text=Hello..."
  -H "Authorization: TOKEN"
```

> Validation errors

```json
{
  "text":[
    "is required",
    "must be 1000 characters or less"
  ]
}
```

Use this route to send a support ticket to the Noncents #support Slack channel. Any block of text may be passed in, but that text must be limited to 1000 characters or less. The User's identifying information is passed along automatically, so there is no need to include anything in the payload other than the support text.

### HTTP Request

`POST ...api/v1/users/me/support`

### URL Parameters

Parameter | Validations | Description
--------- | ----------- | -----------
text | No more than 1000 characters  | Body of support message

## (Dev) Populate Sample Data

```shell
curl -X POST "...api/v1/users/me/dev_populate"
  -H "Authorization: TOKEN"
```

> Successful response:

```json
{
  "id":"7d966671-e36e-5f42-8ed4-fb56cf2f2768",
  "fname":"Cash",
  "lname":"Money",
  "created_at":"2016-05-16T11:24:33.873-08:00",
  "updated_at":"2016-05-16T11:24:33.873-08:00",
  "email":"cashmoney@gmail.com",
  "dob":"1990-01-20",
  "invest_percent":10,
  "sync_date":null,
  "goal":230,
  "phone":"5555552016",
  "fund":{
    "id":"9bf406fc-cc64-45e2-b536-df9f1b0caa4a",
    "balance":"1.53",
    "user_id":"7d966671-e36e-5f42-8ed4-fb56cf2f2768",
    "created_at":"2016-05-16T11:24:33.873-08:00",
    "updated_at":"2016-05-16T11:24:33.873-08:00",
    "amount_invested":"0.53"
  },
  "address":{
    "id":"9bf406fc-cc64-45e2-b536-df9f1b0caa4a",
    "line1":"123 Cashmoney Lane",
    "line2":"Apt 420",
    "city":"Los Angeles",
    "state":"CA",
    "zip":"90024",
    "user_id":"7d966671-e36e-5f42-8ed4-fb56cf2f2768",
    "created_at":"2016-07-20T16:53:30.027-07:00",
    "updated_at":"2016-07-20T16:53:30.027-07:00"
  },
  "accounts":[,
    {
      "id":"3dce9e2f-5321-431d-bd67-9ab3db32a4d3",
      "created_at":"2016-02-19T11:25:18.179-08:00",
      "updated_at":"2016-02-19T11:25:18.179-08:00",
      "plaid_id":"QPO8Jo8vdDHMepg41PBwckXm4KdK1yUdmXOwK",
      "name":"Plaid Savings",
      "institution":"fake_institution",
      "available_balance":null,
      "current_balance":null,
      "account_type":"depository",
      "account_subtype":"savings",
      "user_id":"7d966671-e36e-5f42-8ed4-fb56cf2f2768",
      "bank_id":"e780c643-5006-4730-8055-383ae8e97978",
      "tracking":false,
      "dwolla_id":"97ba8ac0-27ef-45d9-a611-d2a4896b8332",
      "account_num":"9900009606",
      "routing_num":"021000021"
    }
    "..."
  ],
  "transactions":[
    {
      "id":"9bf406fc-cc64-45e2-b536-df9f1b0caa4a",
      "plaid_id":"foo",
      "date":"2015-05-16",
      "amount":"13.37",
      "name":"Python Sticker",
      "category_id":"19013000",
      "account_id":"3dce9e2f-5321-431d-bd67-9ab3db32a4d3",
      "created_at":"2016-05-16T11:24:33.873-08:00",
      "updated_at":"2016-05-16T11:24:33.873-08:00",
      "user_id":"7d966671-e36e-5f42-8ed4-fb56cf2f2768",
      "invested":false,
      "backed_out":false,
      "amount_invested":"0.0",
      "vice":"Electronics"
    },
    "..."
  ],
  "agexes":["..."],
  "vices":[
    "CoffeeShops",
    "Electronics"
  ],
  "yearly_funds":[
    {
      "id":"9bf406fc-cc64-45e2-b536-df9f1b0caa4a",
      "balance":"1.53",
      "amount_invested":"0.53",
      "year":2016,
      "user_id":"7d966671-e36e-5f42-8ed4-fb56cf2f2768",
      "created_at":"2016-05-16T11:24:33.873-08:00",
      "updated_at":"2016-05-16T11:24:33.873-08:00"
    }
  ]
}
```

This route is only for development purposes and will be removed in the future. It fills the authed User's properties with sample data. To do this, it resets the User's Fund balances and destroys all of their existing Vices, Banks, Accounts, and Transactions, replacing them with sample models. These sample models demonstrate things like having multiple Accounts and Vices, backing out of Transactions, having invested Transactions, and having older (more than 2 weeks old) Transactions.

### HTTP Request

`POST ...api/v1/users/me/dev_populate`

## (Dev) Deduct

```shell
curl -X POST "...api/v1/users/me/dev_deduct"
  -H "Authorization: TOKEN"
```

> Successful response:

```json
{
  "id":"7d966671-e36e-5f42-8ed4-fb56cf2f2768",
  "fname":"Cash",
  "lname":"Money",
  "created_at":"2016-02-19T11:24:33.873-08:00",
  "updated_at":"2016-02-19T11:24:33.873-08:00",
  "email":"cashmoney@gmail.com",
  "dob":"1990-01-20",
  "invest_percent":10,
  "sync_date":"2016-02-19T11:24:33.873-08:00",
  "goal":420,
  "phone":"5555552016",
  "fund":{
    "id":"9bf406fc-cc64-45e2-b536-df9f1b0caa4a",
    "balance":"230.72",
    "user_id":"7d966671-e36e-5f42-8ed4-fb56cf2f2768",
    "created_at":"2016-02-19T11:24:33.873-08:00",
    "updated_at":"2016-02-19T11:24:33.873-08:00",
    "amount_invested":"230.72"
  },
  "address":"...",
  "accounts":["..."],
  "agexes":["..."],
  "transactions":[
    {
      "id":"9bf406fc-cc64-45e2-b536-df9f1b0caa4a",
      "plaid_id":"KdDjmojBERUKx3JkDdO5IaRJdZeZKNuK4bnKJ1",
      "date":"2014-06-23",
      "amount":"2307.15",
      "name":"Apple Store",
      "category_id":"19013000",
      "account_id":"3dce9e2f-5321-431d-bd67-9ab3db32a4d3",
      "created_at":"2016-02-19T11:24:33.873-08:00",
      "updated_at":"2016-02-19T11:24:33.873-08:00",
      "user_id":"7d966671-e36e-5f42-8ed4-fb56cf2f2768",
      "invested":true,
      "backed_out":false,
      "amount_invested":"230.72",
      "vice":"Electronics"
    },
    "..."
  ],
  "vices":["..."],
  "yearly_funds":[
    {
      "id":"9bf406fc-cc64-45e2-b536-df9f1b0caa4a",
      "balance":"230.72",
      "amount_invested":"230.72",
      "year":2016,
      "user_id":"7d966671-e36e-5f42-8ed4-fb56cf2f2768",
      "created_at":"2016-02-19T11:24:33.873-08:00",
      "updated_at":"2016-02-19T11:24:33.873-08:00"
    }
  ]
}
```

This route is only for development purposes and will be removed in the future. It travels to each of the transactions in User.transactions and "deducts" money from them, setting the transaction's 'invested' field to true and depositing (Transaction.amount * User.invest_percent/100) dollars into User.fund.amount_invested, User.yearly_fund().amount_invested and Transaction.amount_invested.

One exception is that if the Transaction's 'backed_out' field is true, the 'invested' field will stay false and no money will be deposited into the funds.

### HTTP Request

`POST ...api/v1/users/me/dev_deduct`

## (Dev) Aggregate Old Transactions

```shell
curl -X POST "...api/v1/users/me/dev_aggregate"
  -H "Authorization: TOKEN"
```

> Successful response:

```json
{
  "id":"7d966671-e36e-5f42-8ed4-fb56cf2f2768",
  "fname":"Cash",
  "lname":"Money",
  "created_at":"2016-02-19T11:24:33.873-08:00",
  "updated_at":"2016-02-19T11:24:33.873-08:00",
  "email":"cashmoney@gmail.com",
  "dob":"1990-01-20",
  "invest_percent":10,
  "sync_date":"2016-02-19T11:24:33.873-08:00",
  "goal":420,
  "phone":"5555552016",
  "fund":"...",
  "address":"...",
  "accounts":["..."],
  "agexes":[
    {
      "id":"9bf406fc-cc64-45e2-b536-df9f1b0caa4a",
      "user_id":"7d966671-e36e-5f42-8ed4-fb56cf2f2768",
      "amount":"230.72",
      "month":"2016-02-01",
      "created_at":"2016-02-19T11:24:33.873-08:00",
      "updated_at":"2016-02-19T11:24:33.873-08:00",
      "vice":"Electronics"
    },
    "..."
  ],
  "transactions":["..."],
  "vices":["..."],
  "yearly_funds":["..."]
}
```

This route is only for development purposes and will be removed in the future. It finds all transactions older than a month and aggregates them. It does this by storing them in an Agex model and then deleting them, leaving only transactions for the current month.

"Agex" is a portmanteau of "Aggregate Expenditure" and is used to represent the combination of invested transactions, by vice, for a given month. Accordingly, it has an 'amount' field, a 'vice' field, and a 'month' field (in the format YYYY-MM-01).

This endpoint travels to each of the transactions in User.transactions and checks to see whether the Transaction was invested or not. If so, it looks for how much was invested and then adds that to the existing Agex model for the Transaction's associated month and vice, or creates a new Agex model if no such instance of it exists. Once completed, it removes all of those Transaction models (whether they were invested or not).

### HTTP Request

`POST ...api/v1/users/me/dev_aggregate`

## (Dev) Notify

```shell
curl -X POST "...api/v1/users/me/dev_notify"
  -H "Authorization: TOKEN"
```

> Successful response:

```json
{
  "notification":"sent"
}
```

> Notification format:

```json
{
  "to":"user_1",
  "data":{
    "hello": "world",
    "fname": "Cash",
    "lname": "Money"
  }
}
```

This route is only for development purposes and will be removed in the future. It sends a test notification to the authenticated User.

The notification is currently sent via Firebase using their notification format. This format includes a `data` field, which is essentially just a set of JSON for the client to interpret. For this test endpoint, the data field includes a "hello world" key-value pair, as well as key-value pairs for the authenticated User's first and last name fields.

In order to actually receive notifications, you must first use the `POST .../api/v1/users/me/register_push_token` route to register your FCM token for push notifications. See the `Register for FCM Notifications` section of the documentation for more details.

### HTTP Request

`POST ...api/v1/users/me/dev_notify`
