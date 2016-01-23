# Authentication

The Dimention API uses API keys to allow access to the API. To acquire an API key, you will need to verify your authenticity by requesting an SMS confirmation code at `/confirmation`. Once the client obtains this code via SMS, it will need to be send to `/auth`. If successful, the server will return a JSON User model containing a token that will allow for further API authentication. Look at the bar on the right for more information.

The API expects for the auth token to be included in authenticated API requests to the server. You should include this in a header that looks like the following:

`Authorization: TOKEN`

<aside class="notice">
You must replace <code>TOKEN</code> with your personal API key.
</aside>

## Send SMS Confirmation

```shell
curl "...api/v1/users"
```

> Successful response:

```json
{
  "confirmation": "sent"
}
```

> Invalid phone number:

```json
{
  "confirmation": "invalid"
}
```

Sends an SMS containing a 6-digit confirmation code to the given phone number.

### HTTP Request

`GET ...api/v1/confirmation`

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
number | true | The number to send the 6-digit SMS confirmation code to.

## Get Token

```shell
curl "...api/v1/auth"
```

> Successful response:

```json
{
  "id": 2,
  "fname": "Ethan",
  "lname": "Held",
  "number": "+12146163710",
  "address": "123 Some St.",
  "city": "Los Angeles",
  "state": "CA",
  "zip": "90024",
  "dob": "2000-01-01",
  "accounts":
  [
    "1234",
    "5678"
  ],
  "token": "abc123..."
}
```

> Invalid code or phone number:

```json
{
  "confirmation": "rejected"
}
```

> Other error responses:

```plaintext
"This call requires a confirmation code"
"This call requires a phone number"
```

Accepts a 6-digit confirmation code and a phone number and, if successful, returns the User model corresponding to the phone number in addition to that user's token.

<aside class="warning">If you're not using an administrator API key, note that some calls will return 403 Forbidden if they are hidden for the given user.</aside>

### HTTP Request

`GET ...api/v1/auth`

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
code | true | 6-digit confirmation code
number | true | Phone number of the associated User

## Sign Up

```shell
curl "...api/v1/signup"
```

> Successful response:

```json
{
  "id": 2,
  "fname": "Ethan",
  "lname": "Held",
  "number": "+12146163710",
  "address": "123 Some St.",
  "city": "Los Angeles",
  "state": "CA",
  "zip": "90024",
  "dob": "2000-01-01",
  "accounts":
  [
    "1234",
    "5678"
  ],
  "token": "abc123..."
}
```

> Invalid code or phone number:

```json
{
  "confirmation": "rejected"
}
```

> Other error responses:

```plaintext
"This call requires a confirmation code"
"This call requires a name and phone number"
```

Creates a new User. Accepts a 6-digit confirmation code, a phone number, a first name, and a last name, and, if successful, returns the created User model (or idempotently, the User model corresponding to the phone number if the User already exists) in addition to that user's token.

### HTTP Request

`GET ...api/v1/signup`

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
code | true | 6-digit confirmation code
number | true | Phone number of the associated User
fname | true | The User's first name
lname | true | The User's last name
