---
title: API Reference

language_tabs:
  - shell
  - python

toc_footers:
  - <a href='http://www.bookalimo.com/connect-with-us/'>Contact Us for a Developer Key</a>

includes:

search: true
---

# Introduction

Welcome to the International Chauffeured Service API! You can use our API to get our rates for Point to Point, Hourly and Daily car bookings. You can make a booking via ICS API.

We have language bindings in Shell and Python. You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Get Car Prices
```shell
curl -X POST  "https://e-zbookings.com/api/v1/carprice" \
-H "Content-Type: application/json" \
-d '
{
	"type": "PP",
	"passengers": 1,
	"luggage": 1,
	"passenger": {
		"name_last": "Jones",
		"email": "njones@test.com",
		"name_first": "Nick",
		"phone": "(555) 686-5235"
	},
	"time": "13:52",
	"pickup": {
		"isairport": "true",
		"airportcode": "JFK",
		"airlinecode": "DL",
		"flightno": "234",
		"countrycode": "US"
	},
	"date": "2015-06-29",
	"dropoff": {
		"countrycode": "US",
		"address": "32 bedford rd",
		"zipcode": "10514",
		"state": "NY",
		"isairport": "false"
		"locality": "Chappaqua"
	}
}
'
```
```python
def get_car_prices():
    data = {
       "type": "PP",
       	"passenger": {
       		"name_last": "Jones",
       		"email": "njones@test.com",
       		"name_first": "Nick",
       		"phone": "(555) 686-5235"
       	},
       	"time": "13:52",
       	"pickup": {
       		"airportcode": "EWR",
       		"countrycode": "US",
       		"isairport": "true",
       		"locality": "NYC"
       	},
       	"date": "2015-06-29",
       	"dropoff": {
       		"countrycode": "US",
		"address": "73 S Bedford",
       		"zipcode": "10514",
       		"state": "NY",
       		"isairport": "false",
       		"locality": "Chappaqua"
       	}
    }
    
    json_data               = json.dumps(data)
    post_data               = json_data.encode('utf-8')
    headers                 = {}
    headers['Content-Type'] = 'application/json'
    url                     = 'https://e-zbookings.com/api/v1/carprice'
    req                     = urllib2.Request(url, post_data, headers)  
    res                     = urllib2.urlopen(req)
    result                  = res.read()

    print 'POST https://e-zbookings.com/api/v1/carprice' 
    pp                      = pprint.PrettyPrinter(indent=4)
    json_object             = json.loads(result)
    pp.pprint(json_object)
    print "\n"

    if 'token' in json_object:
        result_token        = json_object ['token']
        global token_id 
        token_id            = result_token
    else:
         print 'Token is null'
```

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

`POST https://e-zbookings.com/api/v1/carprice`

Gets prices for specified pick up and drop off location for different Car Classes and Meet and Greet Options

### Request Parameters

Parameter | Required | Description
--------- | ------- | -----------
passenger | true | Passenger information that includes his name and contact info (see below)
type | true | Point to Point (PP) or Hourly (HR)
hours | only if type=HR | Number of hours for hourly jobs
date | true | Date of the Pick Up
time | true | Time of the Pick Up
pickup | true | Pick Up Location
dropoff | true | Drop Off Location
passengers | false | Number of Passengers, defaults to 1 if skipped
luggage | false | Number of Luggage itesm, defaults to 1 if skipped


### Passenger Parameters

Parameter | Required | Description
--------- | ------- | -----------
name_last | true | Passenger Last Name
name_first | true | Passenger First Name
email | true | Passenger email address
phone | true | Passenger phone number


### Location Parameters
Parameter | Required | Description
--------- | ------- | -----------
isairport | true | Location is an airport "true" or "false"
countrycode | true | Country Code
airportcode | isairport | Airport IATA code, only required when isairport="true"
airlinecode | isairport | Airline IATA code, please refer to [IATA Airline/Airport Search](http://www.iata.org/publications/Pages/code-search.aspx)
flightno | isairport | Flight no, only required when isairport="true"
state | only if countrycode="US" and !isairport | US State, required only when isairport="false" and countrycode is "US"
locality | !isairport | City or Locality
zipcode | !isairport | Postal or Zip Code


Returns a Car Classes with Prices and Meet and Greet Options along with the token that serves as Booking identifier for further requests


This endpoint provides quotes for different car classes and meet and greet options

# Preview Booking

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
```python
def get_preview_booking():
    data      = token_id
    udata     = data.decode("utf-8")
    asciidata = udata.encode("ascii","ignore")
    data      = {
        "token": asciidata,
        "car": "SD",
        "option": "B"
    }
    
    json_data               = json.dumps(data)
    post_data               = json_data.encode('utf-8')
    headers                 = {}
    headers['Content-Type'] = 'application/json'
    url                     = 'https://e-zbookings.com/api/v1/book'
    req                     = urllib2.Request(url, post_data, headers)  
    res                     = urllib2.urlopen(req)
    result                  = res.read()
    pp = pprint.PrettyPrinter(indent = 4)
    print 'POST https://e-zbookings.com/api/v1/book'
    json_object             = json.loads(result)
    pp.pprint(json_object)
    print "\n"

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

# Authentication

ICS uses API keys to allow access to the API. You can get ICS API key by contacting us at http://bookalimo.com/connect-with-us

We expect for the API credentials to be included only in the Confirm Booking request to the server in a header that looks like the following:

`Authorization: Basic base64encodedkeyandsecret`

<aside class="notice">
You must replace <code>base64encodedkeyandsecret</code> with your personal API credentials.
</aside>

# Confirm Booking
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
```python
def get_confirm_booking():
    data = {
        "token": token_id,
            "payment": 
            {
                "type": "VI",
                "cc": "4111111111111111",
                "exp": "1115",
                "zip": "10001",
                "cvv": "123"
           }
    }
            
    json_data                = json.dumps(data)
    post_data                = json_data.encode('utf-8')
    headers                  = {}
    headers['Content-Type']  = 'application/json'
    headers['Authorization'] = 'Basic base46encodedkeyandsecret'
    url                      = 'https://e-zbookings.com/api/v1/pay'
    req                      = urllib2.Request(url, post_data, headers)  
    res                      = urllib2.urlopen(req)
    result                   = res.read()
    pp                       = pprint.PrettyPrinter(indent = 4)
    print 'POST https://e-zbookings.com/api/v1/pay' 
    json_object              = json.loads(result)
    pp.pprint(json_object)
```
> Upon Successful booking the Request above will return following JSON:

```json
{
  "jobId": 658068
}
```
> Where jobId is reservation confirmation number
> Upon a Credit Card Validation problem the JSON response:

```json
{
  "errors":
	[ "Invalid Credit Card" ]
}
```

`POST https://e-zbookings.com/api/v1/pay`



This request requires Authentication Header comprised of your API key and secret

### Request Parameters

Parameter | Required | Description
--------- | ------- | -----------
token | true | A token of the reservation provided by Get Car Prices Response
payment | true | Credit card payment details




