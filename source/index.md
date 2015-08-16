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
`POST https://e-zbookings.com/api/v1/carprice`

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
		"countrycode": "US",
		"isairport": "true",
		"countryname": "United States",
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
Gets prices for specified pick up and drop off location for different Car Classes and Meet and Greet Options


Parameter | Required | Description
--------- | ------- | -----------
passenger | true | Passenger information that includes his name and contact info
type | true | Point to Point (PP), Hourly (HR) or Daily (DL)
date | true | Date of the Pick Up
time | true | Time of the Pick Up
pickup | true | Pick Up Location
dropoff | true | Drop Off Location


Returns a Car Classes with Prices and Meet and Greet Options along with the token that serves as Booking identifier for further requests
> The above command returns JSON structured like this:

```json
{
    "token": "t122so3d90pj9hrqbb4nv7lv2f",
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

# Preview Booking Request

`POST https://e-zbookings.com/api/v1/book`

```shell
curl -X POST "https://e-zbookings.com/api/v1/book" \
  -H "Content-Type: application/json" \
  -d '
{
    "token": "t122so3d90pj9hrqbb4nv7lv2f",
    "car": "SD",
    "option": "C"
}
'
```

Requests a final quote breakdown

### Request Parameters

Parameter | Required | Description
--------- | ------- | -----------
token | true | A token of the reservation provided by Get Car Prices
car | true | Selected Car Class to be used as means of transpiration
option | true | Selected Airport Meet & Greet Option





> The above command returns JSON structured like this:

```json
{
  "token": "t122so3d90pj9hrqbb4nv7lv2f",
  "amount_units": "USD",
  "price": {
    "base_fare": "$127.00",
    "gratuity": "$25.40",
    "toll_misc": "$9.50",
    "parking": "N/A",
    "meet_greet": "$0.00",
    "stc_charge": "$16.03",
    "wc_tax": "$4.45",
    "total": "$182.38",
    "misc": "N/A"
  }
}
```

# Confirm Booking with Payment Information

`POST https://e-zbookings.com/api/v1/pay`

```shell
curl -X POST "https://e-zbookings.com/api/v1/pay" \
  -H "Content-Type: application/json" \
  -H "Authorization: Basic base64encodedkeyandsecret" \
  -d '
{
    "token": "t122so3d90pj9hrqbb4nv7lv2f",
    "payment": {
        "type": "VI",
        "cc": "4111111111111111",
        "exp": "1115",
        "zip": "10001",
        "cvv": "123"
    }
}
'
```
This request requires Authentication Header comprised of your API key and secret

### Request Parameters

Parameter | Required | Description
--------- | ------- | -----------
token | true | A token of the reservation provided by Get Car Prices Response
payment | true | Credit card payment details



<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>




