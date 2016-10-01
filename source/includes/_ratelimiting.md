# Rate Limiting

Rate limiting is performed on several routes, and is done on either a per-IP or per-email basis. The rate limits are given to the right.

Whenever you exceed the rate limit, you will receive an HTTP status code of 429 as well as a body saying:

`429  (Rate Limit Exceeded)`

```shell
300 requests every 5 minutes per IP
5 requests of the /v1/auth route every 20 seconds per IP
5 requests of the /v1/auth route every 20 seconds per email
```
