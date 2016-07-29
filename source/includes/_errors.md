# Errors

The Noncents API uses the following error codes:

Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request sucks
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You are not allowed to access the requested resource
404 | Not Found -- Some or all of your query could not be found
420 | Enhance Your Calm -- You are being rate limited
422 | Unprocessable Entity -- Validation for the given model failed
500 | Internal Server Error -- The problem is with the server, not the client
503 | Service Unavailable -- Temporarily offline for maintenance
