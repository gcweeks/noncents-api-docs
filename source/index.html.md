---
title: Noncents API Reference

toc_footers:
  - <a href='#'>Noncents</a>

includes:
  - authentication
  - ratelimiting
  - general
  - users
  - vices
  - transactions
  - errors

search: true
---

# Introduction

Welcome to the Noncents API documentation.

The app for the production API is located at the following URL:

`https://app.dimention.co/`

The production app can also be found at the AWS Elastic Beanstalk URL:

`https://dimention-env-vd3evffjxi.elasticbeanstalk.com/`

The development API is located at the following URL:

`https://noncents-env-dev.us-east-1.elasticbeanstalk.com`

The API is located at `/api` and is versioned (`/api/v1`, etc). Because there is only one version at the moment, this means you should access all production API calls at the following URL:

`https://app.dimention.co/api/v1`

In the proceeding documentation, this URL will be abbreviated as:

`...api/v1/some_route`

To get a feel for the API, try the sample requests given in the bar to the right.

## Sample GET

```shell
curl "...api/v1"
```

> Response:

```json
{
  "body": "GET Request"
}
```

This endpoint returns a constant JSON string and can be used to test API connectivity.

### HTTP Request

`POST ...api/v1`

## Sample POST

```shell
curl "...api/v1"
  -d "foo=bar"
```

> Response:

```json
{
  "body": "POST Request: foo=bar"
}
```

This endpoint returns the body of the POST request you send, and can be used to test API connectivity.

### HTTP Request

`POST ...api/v1`
