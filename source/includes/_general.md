# General

The following are general API calls that don't fall into any other category.

## iOS Version

```shell
curl -X GET "...v1/version/ios"
```

> Response:

```json
{
  "version": "0.0.1"
}
```

Retrieves the minimum version of the iOS app that is compatible with the current API. This allows the app to check for the minimum version on launch and then prompt the user to update if their app is out of date.

### HTTP Request

`GET ...v1/version/ios`
