# Users

## Check Email

```shell
curl -X GET "...v1/check_email"
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

`GET ...v1/check_email`

### Query Parameters

Parameter | Validations | Description
--------- | ----------- | -----------
email | Present | The User's email

## Sign Up

```shell
curl -X POST "...v1/users"
  -d "user[fname]=Cash&
  user[lname]=Money&
  user[email]=cashmoney%40gmail.com&
  user[password]=Ca5hM0n3y&
  user[dob]=1990-01-20&
  user[invest_percent]=10&
  user[goal]=420&
  user[phone]=5555552016"
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
  "transactions_refreshed_at":null,
  "goal":420,
  "phone":"5555552016",
  "created_at":"2016-02-19T11:24:33.873-08:00",
  "updated_at":"2016-02-19T11:24:33.873-08:00",
  "dwolla_status":null,
  "dwolla_verified_at":null,
  "accounts":[],
  "address":null,
  "agexes":[],
  "deposit_account":null,
  "fund":null,
  "source_account":null,
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

`POST ...v1/users`

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
curl -X GET "...v1/users/me"
  -H "Authorization: TOKEN"
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
  "dwolla_verified_at":"2016-02-19T11:24:33.873-08:00",
  "accounts":["..."],
  "address":"...",
  "agexes":["..."],
  "deposit_account":"...",
  "fund":"...",
  "source_account":"...",
  "transactions":["..."],
  "vices":["..."],
  "yearly_funds":["..."]
}
```

Retrieves the authenticated User

### HTTP Request

`GET ...v1/users/me`

## Update Authenticated User

```shell
curl -X PUT "...v1/users/me"
  -d "user[fname]=New&user[lname]=Name"
  -H "Authorization: TOKEN"
```

> Successful response:

```json
{
  "id":"7d966671-e36e-5f42-8ed4-fb56cf2f2768",
  "fname":"New",
  "lname":"Name",
  "email":"cashmoney@gmail.com",
  "dob":"1990-01-20",
  "invest_percent":10,
  "transactions_refreshed_at":"2016-02-19T11:24:33.873-08:00",
  "goal":420,
  "phone":"5555552016",
  "created_at":"2016-02-19T11:24:33.873-08:00",
  "updated_at":"2016-02-19T11:24:33.873-08:00",
  "dwolla_status":"verified",
  "dwolla_verified_at":"2016-02-19T11:24:33.873-08:00",
  "accounts":["..."],
  "address":"...",
  "agexes":["..."],
  "deposit_account":"...",
  "fund":"...",
  "source_account":"...",
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

`PUT ...v1/users/me`

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
curl -X GET "...v1/users/me/yearly_fund"
  -H "Authorization: TOKEN"
```

> Successful response:

```json
{
  "id":"7d966671-e36e-5f42-8ed4-fb56cf2f2768",
  "balance":"1.53",
  "amount_invested":"0.53",
  "year":2016,
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

`GET ...v1/users/me/yearly_fund`

## Set User Vices

```shell
curl -X PUT "...v1/users/me/vices"
  -d "vices[]=Travel&vices[]=Nightlife"
  -H "Authorization: TOKEN"
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
  "dwolla_verified_at":"2016-02-19T11:24:33.873-08:00",
  "accounts":["..."],
  "address":"...",
  "agexes":["..."],
  "deposit_account":"...",
  "fund":"...",
  "source_account":"...",
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

Sets the authenticated User's Vices. The list of available Vices is given below, and can optionally be obtained by making a call to `GET ...v1/vices`. It is worth noting that this call will overwrite the User's existing Vices, so if the goal is to add one Vice, you must first obtain the original list of Vices and then send the augmented list of Vices as a payload to this endpoint. To clear all Vices, simply pass in a Vice of 'None'.

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

`POST ...v1/users/me/vices`

### URL Parameters

Parameter | Validations | Description
--------- | ----------- | -----------
vices[] | Equal to any of the Vices from the list above | The list of Vices to set for the User

## Set User Address

```shell
curl -X PUT "...v1/users/me/address"
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
  "email":"cashmoney@gmail.com",
  "dob":"1990-01-20",
  "invest_percent":10,
  "transactions_refreshed_at":"2016-02-19T11:24:33.873-08:00",
  "goal":420,
  "phone":"5555552016",
  "created_at":"2016-02-19T11:24:33.873-08:00",
  "updated_at":"2016-02-19T11:24:33.873-08:00",
  "dwolla_status":"verified",
  "dwolla_verified_at":"2016-02-19T11:24:33.873-08:00",
  "accounts":["..."],
  "address":{
    "id":"9bf406fc-cc64-45e2-b536-df9f1b0caa4a",
    "line1":"123 Cashmoney Lane",
    "line2":"Apt 420",
    "city":"Los Angeles",
    "state":"CA",
    "zip":"90024",
    "created_at":"2016-07-20T16:53:30.027-07:00",
    "updated_at":"2016-07-20T16:53:30.027-07:00"
  },
  "agexes":["..."],
  "deposit_account":"...",
  "fund":"...",
  "source_account":"...",
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

`PUT ...v1/users/me/address`

### URL Parameters

Parameter | Validations | Description
--------- | ----------- | -----------
address[line1] | Present  | The street address
address[line2] | Optional | Second line for street address, for things like apartment numbers
address[city]  | Present  | The city
address[state] | Present  | The state
address[zip]   | Present  | The postal code

## Set Monthly Feeling

```shell
curl -X PUT "...v1/users/me/feeling"
  -d "month=2016-12-01&feeling=2"
  -H "Authorization: TOKEN"
```

> Successful response:

```json
[
  {
    "feeling": 2,
    "id":"9bf406fc-cc64-45e2-b536-df9f1b0caa4a",
    "amount":"230.72",
    "month":"2016-02-01",
    "created_at":"2016-02-19T11:24:33.873-08:00",
    "updated_at":"2016-02-19T11:24:33.873-08:00",
    "vice":"Electronics"
  },
  "..."
]
```

> Validation errors

```json
{
  "month":[
    "is required",
    "must be in format YYYY-MM-DD"
  ],
  "feeling":[
    "is required",
    "must be a number between 0 and 5"
  ]
}
```

Sets the User's feeling about their monthly spending by setting a "feeling" field on each Agex associated with that month. If there are no Agexes for the chosen month, this route will do nothing and return a 200.

The feeling is represented by a number from 0 to 3. '0' represents no feeling, and is the default value when an Agex is created. '1' through '5' represent the User's feeling about the current month. For example, Bad (1), Okay (3), and Great (5).

### HTTP Request

`PUT ...v1/users/me/feeling`

### URL Parameters

Parameter | Validations | Description
--------- | ----------- | -----------
month | String in the form of YYYY-MM-DD | Month for which feeling applies
feeling | Integer between 0 and 5 | Integer represent User's feeling

## Create Plaid Account

```shell
curl -X POST "...v1/users/me/plaid"
  -d "username=cashmoney&
  password=Ca5hM0ney&
  product=connect&
  type=wells"
  -H "Authorization: TOKEN"
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
  "dwolla_verified_at":"2016-02-19T11:24:33.873-08:00",
  "accounts":[
    {
      "id":"3dce9e2f-5321-431d-bd67-9ab3db32a4d3",
      "name":"Plaid Savings",
      "institution":"fake_institution",
      "available_balance":null,
      "current_balance":null,
      "account_type":"depository",
      "account_subtype":"savings",
      "tracking":false,
      "bank_id":"e780c643-5006-4730-8055-383ae8e97978",
      "created_at":"2016-02-19T11:24:33.873-08:00",
      "updated_at":"2016-02-19T11:24:33.873-08:00",
      "account_num_short":"1234",
      "plaid_auth":false,
      "plaid_connect":true,
      "plaid_needs_reauth":false
    },
    "..."
  ],
  "address":"...",
  "agexes":["..."],
  "deposit_account":"...",
  "fund":"...",
  "source_account":"...",
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

> If the bank requires a code that they sent to the user's email/phone (Chase only), you will instead be given a list of devices so the user can select which device they want the code sent to

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

> You can then use this information to send the proper call to the POST users/me/plaid_mfa route using the given "mask" or "type" fields

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

> You will need to submit a POST request to the users/me/plaid_mfa route

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
  "product":[
    "is required",
    "must be one of: connect, auth"
  ],
  "type":[
    "is required"
    "<auth> must be one of: bbt, bofa, capone360, schwab, chase, citi,
      fidelity, nfcu, pnc, suntrust, td, us, usaa, wells"
    "<connect> must be one of: amex, bbt, bofa, chase, citi, nfcu, suntrust,
      td, us, usaa, wells"
  ],
  "pin":[
    "is required for usaa"
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

Gets all accounts associated with bank credentials and stores them in the User model and returns them to the client. To perform this call, provide a bank type (listed in the table below), username, password, and product. The product can either be 'auth' or 'connect' (explained below), the names of Plaid's methods of authentication. If the bank type is 'usaa', you must additionally provide a pin. This call is expected to be followed by a call to add these accounts as tracking accounts or as source/deposit accounts for deduction using `PUT ...v1/users/me/accounts`.

In deciding between 'auth' and 'connect', Auth retrieves full account info, including account numbers, so that they may be used with Dwolla to perform movement of money. Connect allows for the retrieval of transactions from the account. Therefore, if the client wishes to both track the spending of a particular account as well as use that account as a source/deposit account for deductions, they most authenticate using both Connect and Auth. To do this, first use this route to authenticate with one product, then use the `POST users/me/plaid_upgrade` route to upgrade the account with the new privilege. In the case that you need both products, Plaid recommends initially authorizing with Auth and then following up with Connect in order to minimize the amount of duplicate MFA needed.

### List of Bank Types

Name | Type | PIN | MFA
---- | --- | --- | ---
American Express | amex | No | None
BB&T | bbt | No | Question-based MFA (3 questions)
Bank of America | bofa | No | Question-based MFA (3 questions)
Capital One 360 | capone360 | No | Question-based MFA (1 to 3 questions)
Charles Schwab | schwab | No | None
Chase | chase | No | Code-based MFA
Citi | citi | No | Question-based MFA and selection-based MFA (auth only)
Fidelity | fidelity | No | None
Navy Federal Credit Union | nfcu | No | None
PNC | pnc | No | Question-based MFA (3 questions)
SunTrust | suntrust | No | None
TD Bank | td | No | Question-based MFA (3 questions)
US Bank | us | No | Question-based MFA (1 to 3 questions)
USAA | usaa | Yes | Question-based MFA (3 questions)
Wells Fargo | wells | No | None

### HTTP Request

`POST ...v1/users/me/plaid`

### URL Parameters

Parameter | Validations | Description
--------- | ----------- | -----------
username | Present | The bank username
password | Present | The bank password
product | 'auth' or 'connect' | Whether to Auth (deduction) or Connect (tracking)
type | Present | The bank name
pin | usaa only | The bank pin

## Upgrade Plaid Account

```shell
curl -X POST "...v1/users/me/plaid"
  -d "product=auth&
      account=9bf4...aa4a"
  -H "Authorization: TOKEN"
```

> The JSON response and errors here are identical to those of POST users/me/plaid. To see a list of everything that can be returned, visit the POST users/me/plaid section of the API documentation.

```json
```

> Validation errors

```json
{
  "product":[
    "is required"
    "must be one of: connect, auth"
  ],
  "account":[
    "is required",
    "does not exist",
    "cannot be upgraded",
    "already has Auth",
    "already has Connect"
  ]
}
```

Attempts to upgrade a User's Account to give more information. For example, a Connect account only allows for tracking transactions, but does not give full account numbers and therefore cannot be used with Dwolla to perform source/deposit deduction. To get full account numbers, the Account must be upgraded to contain the Auth product. Similarly, the client may wish to upgrade an Auth account to have Connect privileges so that they have access to that account's transactions.

It is worth noting that it is the User's Bank, not Account, that is actually being upgraded. This means that if a single Bank contains both a checking and savings account, and those accounts have been initially authenticated with the Auth product, when a client upgrades their checking Account to have the Connect product as well, the associated savings Account will also be given the Connect product.

### HTTP Request

`POST ...v1/users/me/plaid_upgrade`

### URL Parameters

Parameter | Validations | Description
--------- | ----------- | -----------
product | 'auth' or 'connect' | Whether to Auth (deduction) or Connect (tracking)
account | Present | The ID of the Account you wish to upgrade

## Submit Plaid MFA

```shell
curl -X POST "...v1/users/me/plaid_mfa"
  -d "access_token=9b97b...265ac&
  product=connect&
  answer=12345687"
  -H "Authorization: TOKEN"
```

> The JSON response and errors here are identical to those of POST users/me/plaid. To see a list of everything that can be returned, visit the POST users/me/plaid section of the API documentation.

```json
```

> Validation errors

```json
{
  "access_token":[
    "is required"
  ],
  "product":[
    "is required",
    "must be one of: connect, auth"
  ],
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

If a call `POST ...v1/users/me/plaid` requires Multi-Factor Authentication (MFA), you will instead have to use this route to successfully connect with the user's bank accounts.

To submit an answer to an MFA question or code, use the `answer` field.

To specify which particular device you would like to receive your code (if doing code-based MFA, i.e. Chase), use the `mask` or `type` fields. The `type` field lets you specify the device type, i.e. "phone" or "email". `mask` lets you get more specific. For example, if the user has multiple phones, you can specify the correct phone number by using `mask=xxx-xxx-5309` in your call. To get a better idea of your options, make sure you've read the returned JSON list of device options in the 'POST users/me/plaid' section of the API documentation.

Just like the 'Post users/me/plaid' route, this call may either return a User model complete with the newly plaid-authenticated accounts, or it may return more MFA.

### HTTP Request

`POST ...v1/users/me/plaid_mfa`

### URL Parameters

Parameter | Validations | Description
--------- | ------- | -----------
access_token | Present | The token received in the returned MFA that you are answering for
product | 'auth' or 'connect' | The product you used when you received a response requesting MFA
answer | Present unless 'mask' or 'type' are present | Answer to the MFA
mask | Present unless 'answer' or 'type' are present | MFA device selection based on device mask
type | Present unless 'mask' or 'answer' are present | The bank password

## Update Plaid Credentials

```shell
curl -X PUT "...v1/users/me/plaid_upgrade"
  -d "username=cashmoney&
      password=Ca5hM0ney&
      bank_id=3dce9...2a4d3"
  -H "Authorization: TOKEN"
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
  "dwolla_verified_at":"2016-02-19T11:24:33.873-08:00",
  "accounts":[
    {
      "id":"3dce9e2f-5321-431d-bd67-9ab3db32a4d3",
      "name":"Plaid Savings",
      "institution":"fake_institution",
      "available_balance":null,
      "current_balance":null,
      "account_type":"depository",
      "account_subtype":"savings",
      "tracking":false,
      "bank_id":"e780c643-5006-4730-8055-383ae8e97978",
      "created_at":"2016-02-19T11:24:33.873-08:00",
      "updated_at":"2016-02-19T11:24:33.873-08:00",
      "account_num_short":"1234",
      "plaid_auth":false,
      "plaid_connect":true,
      "plaid_needs_reauth":false
    },
    "..."
  ],
  "address":"...",
  "agexes":["..."],
  "deposit_account":"...",
  "fund":"...",
  "source_account":"...",
  "transactions":["..."],
  "vices":["..."],
  "yearly_funds":["..."]
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
  "pin":[
    "is required for usaa"
  ],
  "bank_id":[
    "is required"
  ],
  "general":[
    "Bank not in need of update",
    "Bank cannot be updated"
  ]
}
```

When a user changes their password or MFA credentials with a financial institution or is locked out of their account, they must update their credentials with Plaid as well. This route allows the user to re-enter their credentials. To see if a user needs to re-enter their credentials, look through the User's Accounts and check the `Account.plaid_needs_reauth` flag. If set to true, the Bank designated by the `Account.bank_id` field needs to be re-authenticated. Provide the username, password (and pin if USAA bank), and Bank ID to this route to provide Plaid with the new credentials.

### HTTP Request

`PUT ...v1/users/me/plaid_update`

### URL Parameters

Parameter | Validations | Description
--------- | ----------- | -----------
username | Present | The bank username
password | Present | The bank password
pin | usaa only | The bank pin
bank_id | Present | The ID for the Bank in question

## Set Accounts

```shell
curl -X PUT "...v1/users/me/accounts"
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
  "email":"cashmoney@gmail.com",
  "dob":"1990-01-20",
  "invest_percent":10,
  "transactions_refreshed_at":"2016-02-19T11:24:33.873-08:00",
  "goal":420,
  "phone":"5555552016",
  "created_at":"2016-02-19T11:24:33.873-08:00",
  "updated_at":"2016-02-19T11:24:33.873-08:00",
  "dwolla_status":"verified",
  "dwolla_verified_at":"2016-02-19T11:24:33.873-08:00",
  "accounts":["..."],
  "address":"...",
  "agexes":["..."],
  "deposit_account":{
    "id":"3dce9e2f-5321-431d-bd67-9ab3db32a4d3",
    "name":"Plaid Savings",
    "institution":"fake_institution",
    "available_balance":null,
    "current_balance":null,
    "account_type":"depository",
    "account_subtype":"savings",
    "tracking":false,
    "bank_id":"e780c643-5006-4730-8055-383ae8e97978",
    "created_at":"2016-02-19T11:24:33.873-08:00",
    "updated_at":"2016-02-19T11:24:33.873-08:00",
    "account_num_short":"1234",
    "plaid_auth":true,
    "plaid_connect":true,
    "plaid_needs_reauth":false
  },
  "fund":"...",
  "source_account":{
    "id":"9bf406fc-cc64-45e2-b536-df9f1b0caa4a",
    "name":"Plaid Checking",
    "institution":"fake_institution",
    "available_balance":null,
    "current_balance":null,
    "account_type":"depository",
    "account_subtype":"checking",
    "tracking":true,
    "bank_id":"e780c643-5006-4730-8055-383ae8e97978",
    "created_at":"2016-02-19T11:24:33.873-08:00",
    "updated_at":"2016-02-19T11:24:33.873-08:00",
    "account_num_short":"5678",
    "plaid_auth":true,
    "plaid_connect":true,
    "plaid_needs_reauth":false
  },
  "transactions":["..."],
  "vices":["..."],
  "yearly_funds":["..."]
}
```

> Validation errors

```json
{
  "general":[
    "Missing parameter. Options are one or more of: 'source', 'deposit', 'tracking'",
    "User is not yet verified with Dwolla"
  ],
  "source":[
    "Account not found",
    "is incorrectly formatted - must be of type String",
    "type must be one of: savings, checking",
    "must have Plaid Auth product"
  ],
  "deposit":[
    "Account not found",
    "is incorrectly formatted - must be of type String",
    "type must be one of: savings, checking",
    "must have Plaid Auth product"
  ],
  "tracking":[
    "Account not found",
    "is incorrectly formatted - must be of type Array",
    "Account with ID <account id> must have Plaid Connect product"
  ]
}
```

After acquiring all of the user's bank accounts, they need to specify which Accounts they want to track and which they want to use for deduction. For instance, they may want to track spending from a checking account, but not from a savings account at the same bank, and they may want to deduct from their checking account into their savings account every week.

To specify which Accounts to track, pass in an array `tracking[]` that contains the ID of each Account you want to track. To specify an Account to deduct money into each week, pass in the key `deposit` with the ID of the Account as its value. Similarly, for the Account to deduct money from, use the `source` key.

You may use this route do set multiple Accounts at once. For example, you can track multiple Accounts and add the source/deposit Accounts all in one call. This route is also idempotent, meaning that adding Accounts as source/deposit/tracking multiple times will not have any adverse effects. Similarly, passing in a new source/deposit Account will override the previous ones. Passing in a new tracking Account will add it to the array of Accounts to track. If instead you wish to remove a tracking Account, use the `DELETE` REST call for this same route. For more information on deleting Accounts, see the relevant section in the documentation.

To add a source or deposit account, the User must already be authenticated with Dwolla (via the `POST users/me/dwolla` route) and the Account must be authenticated with the Plaid Auth product (if the Account already has the Connect product, it must be upgraded using the `POST users/me/plaid_upgrade` route). To add a tracking account, the Account must be authenticated with the Plaid Connect product (if the Account already has the Auth product, it must be upgraded using the `POST users/me/plaid_upgrade` route).

### HTTP Request

`PUT ...v1/users/me/accounts`

### URL Parameters

Parameter | Validations | Description
--------- | ----------- | -----------
source | String | ID of Account to deduct money from
deposit | String | ID of Account to deposit money into
accounts[] | Array | IDs for Accounts you wish to track

## Remove Accounts

```shell
curl -X DELETE "...v1/users/me/accounts"
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
  "email":"cashmoney@gmail.com",
  "dob":"1990-01-20",
  "invest_percent":10,
  "transactions_refreshed_at":"2016-02-19T11:24:33.873-08:00",
  "goal":420,
  "phone":"5555552016",
  "created_at":"2016-02-19T11:24:33.873-08:00",
  "updated_at":"2016-02-19T11:24:33.873-08:00",
  "dwolla_status":"verified",
  "dwolla_verified_at":"2016-02-19T11:24:33.873-08:00",
  "accounts":["..."],
  "address":"...",
  "agexes":["..."],
  "deposit_account":null,
  "fund":"...",
  "source_account":null,
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

`DELETE ...v1/users/me/accounts`

### URL Parameters

Parameter | Validations | Description
--------- | ----------- | -----------
source | None | Remove the User's source Account
deposit | None | Remove the User's deposit Account
accounts[] | Array | IDs for Accounts you wish to stop tracking

## Create Dwolla Customer

```shell
curl -X POST "...v1/users/me/dwolla"
  -d "ssn=123-45-6789&address[line1]=..."
  -H "Authorization: TOKEN"
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
  "dwolla_verified_at":"2016-02-19T11:24:33.873-08:00",
  "accounts":["..."],
  "address":"...",
  "agexes":["..."],
  "deposit_account":"...",
  "fund":"...",
  "source_account":"...",
  "transactions":["..."],
  "vices":["..."],
  "yearly_funds":["..."]
}
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

This call will return the user model, complete with their Dwolla Customer status `dwolla_status`. This will be equal to one of the following statuses:

Status | Resolution
------ | -----------
verified | No further action necessary
retry | Must resubmit information, either due to typo or misinformation
document | Must submit image of passport, driver's license or ID card
suspended | No further action possible via server, must contact Dwolla

The `retry` status can be resolved by using this same route by passing in the extra parameter `retry=true` and entering correct information.

The `document` status must be resolved by making a `POST` call to the `...v1/users/me/dwolla_document` route with an image of the user's identification as well as the type of that identification. The image must be in one of the following file formats: `.jpg`, `.jpeg`, `.png`, `.tif`, or `.pdf`. The type can be one of: `passport`, `license`, or `idCard`.

### HTTP Request

`POST ...v1/users/me/dwolla`

### URL Parameters

Parameter | Validations | Description
--------- | ----------- | -----------
ssn | Present  | Social security number
address[line1] | Present  | The street address
address[line2] | Optional | Second line for street address, for things like apartment numbers
address[city]  | Present  | The city
address[state] | Present  | The state
address[zip]   | Present  | The postal code
retry | Optional | Whether the client is retrying Dwolla verification

## Submit Dwolla Document

```shell
curl -X POST "...v1/users/me/dwolla_document"
  -d "type=license"
  -H "Authorization: TOKEN"
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
  "dwolla_status":"document",
  "dwolla_verified_at":null,
  "accounts":["..."],
  "address":"...",
  "agexes":["..."],
  "deposit_account":"...",
  "fund":"...",
  "source_account":"...",
  "transactions":["..."],
  "vices":["..."],
  "yearly_funds":["..."]
}
```

> Validation errors

```json
{
  "file":[
    "is required"
  ],
  "document":[
    "is required"
  ]
}
```

Use this route to submit an identifying document to verify a Dwolla Customer. This is required if the client has previously called the `POST ...v1/users/me/dwolla` route and received a `User.dwolla_status` of `document`. The document image must be in one of the following file formats: `.jpg`, `.jpeg`, `.png`, `.tif`, or `.pdf`. The document type must be one of: `passport`, `license`, or `idCard`.

### HTTP Request

`POST ...v1/users/me/dwolla_document`

### URL Parameters

Parameter | Validations | Description
--------- | ----------- | -----------
file | formatted as jpg, jpeg, png, tif, or pdf | Image of identifying document
type | 'passport', 'license', or 'idCard'  | The type of identification

## Refresh Transactions

```shell
curl -X POST "...v1/users/me/refresh_transactions"
  -H "Authorization: TOKEN"
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
  "dwolla_verified_at":"2016-02-19T11:24:33.873-08:00",
  "accounts":["..."],
  "address":"...",
  "agexes":["..."],
  "deposit_account":"...",
  "fund":"...",
  "source_account":"...",
  "transactions":[
    {
      "id":"9bf406fc-cc64-45e2-b536-df9f1b0caa4a",
      "date":"2014-06-23",
      "amount":"2307.15",
      "name":"Apple Store",
      "category_id":"19013000",
      "created_at":"2016-02-19T11:24:33.873-08:00",
      "updated_at":"2016-02-19T11:24:33.873-08:00",
      "invested":false,
      "backed_out":true,
      "amount_invested":"0.0",
      "account_id":"3dce9e2f-5321-431d-bd67-9ab3db32a4d3",
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

`POST ...v1/users/me/refresh_transactions`

## Register for FCM Notifications

```shell
curl -X POST "...v1/users/me/register_push_token"
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

`POST ...v1/users/me/register_push_token`

## Send Slack Support Ticket

```shell
curl -X POST "...v1/users/me/support"
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

`POST ...v1/users/me/support`

### URL Parameters

Parameter | Validations | Description
--------- | ----------- | -----------
text | No more than 1000 characters  | Body of support message

## (Dev) Populate Sample Data

```shell
curl -X POST "...v1/users/me/dev_populate"
  -H "Authorization: TOKEN"
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
  "goal":230,
  "phone":"5555552016",
  "created_at":"2016-05-16T11:24:33.873-08:00",
  "updated_at":"2016-05-16T11:24:33.873-08:00",
  "dwolla_status":"verified",
  "dwolla_verified_at":"2016-02-19T11:24:33.873-08:00",
  "accounts":[
    {
      "id":"3dce9e2f-5321-431d-bd67-9ab3db32a4d3",
      "name":"Plaid Savings",
      "institution":"fake_institution",
      "available_balance":null,
      "current_balance":null,
      "account_type":"depository",
      "account_subtype":"savings",
      "tracking":false,
      "bank_id":"e780c643-5006-4730-8055-383ae8e97978",
      "created_at":"2016-02-19T11:24:33.873-08:00",
      "updated_at":"2016-02-19T11:24:33.873-08:00",
      "account_num_short":"1234",
      "plaid_auth":true,
      "plaid_connect":true,
      "plaid_needs_reauth":false
    }
    "..."
  ],
  "address":{
    "id":"9bf406fc-cc64-45e2-b536-df9f1b0caa4a",
    "line1":"123 Cashmoney Lane",
    "line2":"Apt 420",
    "city":"Los Angeles",
    "state":"CA",
    "zip":"90024",
    "created_at":"2016-07-20T16:53:30.027-07:00",
    "updated_at":"2016-07-20T16:53:30.027-07:00"
  },
  "agexes":["..."],
  "deposit_account":"...",
  "fund":{
    "id":"9bf406fc-cc64-45e2-b536-df9f1b0caa4a",
    "balance":"1.53",
    "amount_invested":"0.53",
    "created_at":"2016-05-16T11:24:33.873-08:00",
    "updated_at":"2016-05-16T11:24:33.873-08:00"
  },
  "source_account":"...",
  "transactions":[
    {
      "id":"9bf406fc-cc64-45e2-b536-df9f1b0caa4a",
      "date":"2015-05-16",
      "amount":"13.37",
      "name":"Python Sticker",
      "category_id":"19013000",
      "created_at":"2016-05-16T11:24:33.873-08:00",
      "updated_at":"2016-05-16T11:24:33.873-08:00",
      "invested":false,
      "backed_out":false,
      "amount_invested":"0.0",
      "account_id":"3dce9e2f-5321-431d-bd67-9ab3db32a4d3",
      "vice":"Electronics"
    },
    "..."
  ],
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
      "created_at":"2016-05-16T11:24:33.873-08:00",
      "updated_at":"2016-05-16T11:24:33.873-08:00"
    }
  ]
}
```

This route is only for development purposes and will be removed in the future. It fills the authed User's properties with sample data. To do this, it resets the User's Fund balances and destroys all of their existing Vices, Banks, Accounts, and Transactions, replacing them with sample models. These sample models demonstrate things like having multiple Accounts and Vices, backing out of Transactions, having invested Transactions, and having older (more than 2 weeks old) Transactions.

### HTTP Request

`POST ...v1/users/me/dev_populate`

## (Dev) Deduct

```shell
curl -X POST "...v1/users/me/dev_deduct"
  -H "Authorization: TOKEN"
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
  "goal":230,
  "phone":"5555552016",
  "created_at":"2016-05-16T11:24:33.873-08:00",
  "updated_at":"2016-05-16T11:24:33.873-08:00",
  "dwolla_status":"verified",
  "dwolla_verified_at":"2016-02-19T11:24:33.873-08:00",
  "accounts":["..."],
  "address":"...",
  "agexes":["..."],
  "deposit_account":"...",
  "fund":{
    "id":"9bf406fc-cc64-45e2-b536-df9f1b0caa4a",
    "balance":"1.53",
    "amount_invested":"0.53",
    "created_at":"2016-05-16T11:24:33.873-08:00",
    "updated_at":"2016-05-16T11:24:33.873-08:00"
  },
  "source_account":"...",
  "transactions":[
    {
      "id":"9bf406fc-cc64-45e2-b536-df9f1b0caa4a",
      "date":"2015-05-16",
      "amount":"13.37",
      "name":"Python Sticker",
      "category_id":"19013000",
      "created_at":"2016-05-16T11:24:33.873-08:00",
      "updated_at":"2016-05-16T11:24:33.873-08:00",
      "invested":false,
      "backed_out":false,
      "amount_invested":"0.0",
      "account_id":"3dce9e2f-5321-431d-bd67-9ab3db32a4d3",
      "vice":"Electronics"
    },
    "..."
  ],
  "vices":["..."],
  "yearly_funds":[
    {
      "id":"9bf406fc-cc64-45e2-b536-df9f1b0caa4a",
      "balance":"1.53",
      "amount_invested":"0.53",
      "year":2016,
      "created_at":"2016-05-16T11:24:33.873-08:00",
      "updated_at":"2016-05-16T11:24:33.873-08:00"
    }
  ]
}
```

This route is only for development purposes and will be removed in the future. It travels to each of the transactions in User.transactions and "deducts" money from them, setting the transaction's 'invested' field to true and depositing (Transaction.amount * User.invest_percent/100) dollars into User.fund.amount_invested, User.yearly_fund().amount_invested and Transaction.amount_invested.

One exception is that if the Transaction's 'backed_out' field is true, the 'invested' field will stay false and no money will be deposited into the funds.

### HTTP Request

`POST ...v1/users/me/dev_deduct`

## (Dev) Aggregate Old Transactions

```shell
curl -X POST "...v1/users/me/dev_aggregate"
  -H "Authorization: TOKEN"
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
  "dwolla_verified_at":"2016-02-19T11:24:33.873-08:00",
  "accounts":["..."],
  "address":"...",
  "agexes":[
    {
      "feeling": 2,
      "id":"9bf406fc-cc64-45e2-b536-df9f1b0caa4a",
      "amount":"230.72",
      "month":"2016-02-01",
      "created_at":"2016-02-19T11:24:33.873-08:00",
      "updated_at":"2016-02-19T11:24:33.873-08:00",
      "vice":"Electronics"
    },
    "..."
  ],
  "deposit_account":"...",
  "fund":"...",
  "source_account":"...",
  "transactions":["..."],
  "vices":["..."],
  "yearly_funds":["..."]
}
```

This route is only for development purposes and will be removed in the future. It finds all transactions older than a month and aggregates them. It does this by storing them in an Agex model and then deleting them, leaving only transactions for the current month.

"Agex" is a portmanteau of "Aggregate Expenditure" and is used to represent the combination of invested transactions, by vice, for a given month. Accordingly, it has an 'amount' field, a 'vice' field, and a 'month' field (in the format YYYY-MM-01).

This endpoint travels to each of the transactions in User.transactions and checks to see whether the Transaction was invested or not. If so, it looks for how much was invested and then adds that to the existing Agex model for the Transaction's associated month and vice, or creates a new Agex model if no such instance of it exists. Once completed, it removes all of those Transaction models (whether they were invested or not).

### HTTP Request

`POST ...v1/users/me/dev_aggregate`

## (Dev) Notify

```shell
curl -X POST "...v1/users/me/dev_notify"
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
    "hello":"world",
    "fname":"Cash",
    "lname":"Money"
  }
}
```

This route is only for development purposes and will be removed in the future. It sends a test notification to the authenticated User.

The notification is currently sent via Firebase using their notification format. This format includes a `data` field, which is essentially just a set of JSON for the client to interpret. For this test endpoint, the data field includes a "hello world" key-value pair, as well as key-value pairs for the authenticated User's first and last name fields.

In order to actually receive notifications, you must first use the `POST ...v1/users/me/register_push_token` route to register your FCM token for push notifications. See the `Register for FCM Notifications` section of the documentation for more details.

### HTTP Request

`POST ...v1/users/me/dev_notify`

## (Dev) Email

```shell
curl -X POST "...v1/users/me/dev_email"
  -H "Authorization: TOKEN"
```

This route is only for development purposes and will be removed in the future. It sends a test email to the email address of the authenticated User.

The email is currently sent via AWS SES and contains a simple welcome message formatted in both HTML and plain text, depending on the recipient's desired format. The email is currently sent from donotreply@noncents.co, and until we are upgraded beyond the AWS SES sandbox, all destination email addresses will first need to be verified via AWS before they can receive mail from this route.

### HTTP Request

`POST ...v1/users/me/dev_email`
