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

The app for the production API is currently located at the following URL:

`https://app.dimention.co/`

The development API is located at the following URL:

`https://app.noncents.co/`

The new production API will be located at:

`https://api.noncents.co/`

For now, the new production API can be used as a development API for testing compliance with the new server setup.

The API is is versioned (`/v1`, `/v2`, etc). Because there is only one version at the moment, this means you should access all production API calls at the following URL:

`https://app.dimention.co/v1`

In the proceeding documentation, this URL will be abbreviated as:

`...v1/some_route`

To get a feel for the API, try the sample requests given in the bar to the right.

## Sample GET

```shell
curl "...v1"
```

> Response:

```json
{
  "body": "GET Request"
}
```

This endpoint returns a constant JSON string and can be used to test API connectivity.

### HTTP Request

`POST ...v1`

## Sample POST

```shell
curl "...v1"
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

`POST ...v1`
