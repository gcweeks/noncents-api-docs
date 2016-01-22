---
title: Dimention API Reference

toc_footers:
  - <a href='#'>Dimention</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Dimention API documentation.

For now, the API is located at the AWS Elastic Beanstalk url:

`http://dimention-env-vd3evffjxi.elasticbeanstalk.com`

The API is located at `/api` and is versioned (`/api/v1`, etc). Because there is only one version at the moment, this means you should access all API calls at the following URL:

`http://dimention-env-vd3evffjxi.elasticbeanstalk.com/api/v1`

In the documentation below, this URL will be abbreviated as:

`...api/v1/some_route`

# Authentication

Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

The API expects for the auth token to be included in most API requests to the server in a header that looks like the following:

`Authorization: TOKEN`

<aside class="notice">
You must replace <code>TOKEN</code> with your personal API key.
</aside>

# Users

## Get All Users

```shell
curl "...api/v1/users"
  -H "Authorization: TOKEN"
```

> JSON Response:

```json
[
  {
    "id": 1,
    "fname": "Chris",
    "lname": "Weeks",
    "number": "+18058233141",
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
  },
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
]
```

This endpoint retrieves all users.

### HTTP Request

`GET ...api/v1/users`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include users that have already been adopted.

<aside class="success">
Remember — a happy user is an authenticated user!
</aside>

## Get a Specific User

```shell
curl "...api/v1/users/2"
  -H "Authorization: TOKEN"
```

> The above command returns JSON structured like this:

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

This endpoint retrieves a specific user.

<aside class="warning">If you're not using an administrator API key, note that some calls will return 403 Forbidden if they are hidden for admins only.</aside>

### HTTP Request

`GET ...api/v1/users/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the user to retrieve
