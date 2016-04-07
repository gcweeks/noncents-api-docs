# Rate Limiting

Rate limiting is done on a per-IP basis. The rate limits are given to the right.

Whenever you exceed the rate limit, you will receive an HTTP status code of 420 as well as a body saying:

`420  (Rate Limit Exceeded)`

```shell
Minute - max: 60 requests
Hourly - max: 1000 requests
```
