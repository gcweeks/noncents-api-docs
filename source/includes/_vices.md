# Vices

## Get a List of Vices

```shell
curl -X GET "...v1/vices"
```

> Successful response:

```json
[
  "Nightlife",
  "Restaurants",
  "Shopping",
  "FastFood",
  "CoffeeShops",
  "Travel",
  "Experiences",
  "Electronics",
  "PersonalCare",
  "Movies",
  "RideSharing"
]
```

Retrieves a list of all of the accepted Vice strings for use with `POST ...v1/users/me/vices`

### HTTP Request

`GET ...v1/vices`
