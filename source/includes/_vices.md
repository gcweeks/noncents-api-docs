# Vices

## Get a List of Vices

```shell
curl "...api/v1/vices"
```

> The above command returns JSON structured like this:

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

Retrieves a list of all of the accepted Vice strings for use with `POST ...api/v1/users/me/vices`

### HTTP Request

`GET ...api/v1/vices`
