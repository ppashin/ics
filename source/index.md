---
title: API Reference

language_tabs:
  - shell

toc_footers:
  - <a href='http://www.bookalimo.com/connect-with-us/'>Sign Up for a Developer Key</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the International Chauffeured Service API! You can use our API to get our rates for Point to Point, Hourly and Daily car bookings. You can make a booking via ICS API.

We have language bindings in Shell. You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](http://github.com/tripit/slate). Feel free to edit it and use it as a base for your own APIs documentation.

# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "https://e-zbookings.com/api/v1"
  -H "Authorization: Basic base64encodedkeyandsecret"
```

> Make sure to replace `base64encodedkeyandsecret` with your API credentials.

ICS uses API keys to allow access to the API. You can get ICS API key by contacting us at http://bookalimo.com/connect-with-us

We expects for the API credentials to be included only in the pay requess to the server in a header that looks like the following:

`Authorization: Basic base64encodedkeyandsecret`

<aside class="notice">
You must replace <code>base64encodedkeyandsecret</code> with your personal API credentials.
</aside>

# Get Car Prices

```shell
curl -X POST  "https://e-zbookings.com/api/v1/carprice" \
-H "Content-Type: application/json" \
-d '
{
	"type": "PP",
	"passenger": {
		"name_last": "Jones",
		"email": "njones@test.com",
		"name_first": "Nick",
		"phone": "(555) 686-5235"
	},
	"time": "13:52",
	"pickup": {
		"airportcode": "JFK",
		"addressFull": "",
		"countrycode": "US",
		"address": "",
		"zipcode": "",
		"state": "NY",
		"isairport": "true",
		"countryname": "United States",
		"locality": "null",
		"longitude": -73.960323,
		"sublocality": "",
		"latitude": 40.64454
	},
	"date": "2015-06-29",
	"dropoff": {
		"airportcode": "null",
		"addressFull": "",
		"countrycode": "US",
		"address": "",
		"zipcode": "10514",
		"state": "NY",
		"isairport": "false",
		"countryname": "United States",
		"locality": "Chappaqua",
		"longitude": -115.176067,
		"sublocality": "null",
		"latitude": 36.09551
	}
}
'
```

> The above command returns JSON structured like this:

```json
{
    "token": "cvjlthkte5lhfj83p4iitovc9j",
    "prices": [
        {
            "id": "1",
            "carClassId": "SD",
            "type": "SEDAN LINCOLN, CADILLAC",
            "price": "127",
            "max_pass": "3",
            "max_lugg": "3"
        },
        {
            "id": "2",
            "carClassId": "BMW",
            "type": "BMW 7 SERIES",
            "price": "212",
            "max_pass": "3",
            "max_lugg": "3"
        },
        {
            "id": "3",
            "carClassId": "MBZ",
            "type": "MERCEDES S CLASS",
            "price": "212",
            "max_pass": "2",
            "max_lugg": "2"
        },
        {
            "id": "4",
            "carClassId": "SUV",
            "type": "SUV 5-6 PASSENGERS",
            "price": "192",
            "max_pass": "6",
            "max_lugg": "10"
        },
        {
            "id": "5",
            "carClassId": "SL6",
            "type": "STRETCH LIMO 6 PASSENGERS",
            "price": "177",
            "max_pass": "6",
            "max_lugg": "5"
        },
        {
            "id": "6",
            "carClassId": "SL8",
            "type": "STRETCH LIMO 8 PASSENGERS",
            "price": "192",
            "max_pass": "8",
            "max_lugg": "5"
        },
        {
            "id": "7",
            "carClassId": "SL10",
            "type": "STRETCH LIMO 10 PASSENGERS",
            "price": "202",
            "max_pass": "10",
            "max_lugg": "5"
        },
        {
            "id": "8",
            "carClassId": "SPT",
            "type": "SPRINTER VAN 14 PASSENGERS",
            "price": "262",
            "max_pass": "12",
            "max_lugg": "14"
        },
        {
            "id": "9",
            "carClassId": "MBUS",
            "type": "MINIBUS 22-36 PASSENGERS",
            "price": "437",
            "max_pass": "36",
            "max_lugg": "24"
        }
    ],
    "options": [
        {
            "id": "O",
            "price": "0",
            "name": "Other"
        },
        {
            "id": "B",
            "price": "15",
            "name": "Baggage Claim"
        },
        {
            "id": "C",
            "price": "0",
            "name": "Curb Side"
        },
        {
            "id": "G",
            "price": "20",
            "name": "Gate"
        },
        {
            "id": "I",
            "price": "20",
            "name": "International"
        }
    ]
}
```

This endpoint provides quotes for different car classes and meet and greet options

# Book Request

`POST https://e-zbookings.com`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Isis",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">If you're not using an administrator API key, note that some kittens will return 403 Forbidden if they are hidden for admins only.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

