---
title: API Reference

language_tabs:
  - ruby

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Shipmnts.com API! You can use our API endpoints to push and retreive information from the various modules we have.

We have language bindings in Ruby. You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](https://github.com/tripit/slate). Feel free to edit it and use it as a base for your own API's documentation.

# Quote requests

## Create New Quote request
```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```


> The above command returns JSON structured like this:

```json
{
  "quote_request": {
  "id": 3,
  "created_at": 1500292868,
  "updated_at": 1500292868,
  "services_requested": ["origin_clearing", "origin_warehousing", "freight"],
  "customer_preferences": null,
  "incoterms": "CIF",
 "port_of_loading": [
  {
    "name": "Ahmedabad",
    "iata_code": "AMD",
    "unloc_code": "INAMD"
  },
  {
    "name": "Mumbai",
    "iata_code": "BOM",
    "unloc_code": "INBOM"
  }
],
"port_of_discharge": [
  { "name": "London Heathrow Airport",
    "iata_code": "LHR",
    "unloc_code": "GBLHR"
  }
],
"origin_address": {
  "id": "90090",
  "name": "Ahmedabad Plant",
  "address_line_1": "A-28 Pariseema Complex",
  "address_line_2": "Opposite Tanishq Showroom",
  "city": "Ahmedabad",
  "state": "Gujarat",
  "country_code": "IN",
  "country": "India",
  "postal_code": "380009"
},
"destination_address": null,
"destuffing_location": null,
"stuffing_location": null,
"cargo_ready_date": 1500292868,
"target_delivery_date": null,
"payment_terms": "30 days",
"gross_weight": 400,
"volumetric_weight": 500,
"weight_unit": "kg",
"gross_volume": 1,
"volume_unit": "CBM",
"valid_till": null
}
}
```

This endpoint creates a new quote request in the organizations procure pipeline.

### HTTP Request

`POST http://localhost:3000/quote_requests`

### Query Parameters

Parameter | Type | Description
--------- | ------- | -----------
collaborating_companies | Array of Hash | Companies which are collaborating on this quote request. Schema definition of the object is defined [here](#collaborating-company-object)
cargo_ready_date | Date | Its the date when the cargo of the shipper is ready
target_delivery_date | Date | Its the date by which the cargo has to reach the destination
service_requested | Array of string | All the services which are required by the company requesting the quote
incoterms | string | Standard incoterms defined internationally
port_of_loading | Array of Hash | Array of all possible Ports from where you want to load the cargo. Object is defined in the example and the schema [here](#port-object)
port_of_discharge | Array of Hash | Array of all possible Ports where the cargo can be discharged. Object is defined in the example and the schema [here](#port-object).
origin_address | Hash | Address from where loose goods are supposed to be picked up.  The schema of address object is defined [here](#address-object)
destination_address | Hash | Address to where cargo is supposed to be delivered. The schema of address object is defined [here](#address-object)
stuffing_location | Object | [Address](#address-object) / [Port](#port-object) where cargo is supposed to be stuff into the containers in the origin country
destuffing_locaiton | Hash | [Address](#address-object) / [Port](#port-object) where cargo is supposed to be destuffed from the containers in the destination country
gross_weight | Decimal | Gross weight of the cargo
volumetric_weight | Decimal | Calculated by using gross weight and volume
weight_unit | String | Weight unit ISO unit codes allowed
gross_volume | Decimal | Gross volume of the cargo
volume_unit  | Decimal | Volume unit ISO unit codes
payment_terms | String | Prepaid, collect, 30 days credit

<aside class="success">
On successful post call response described in the code example section will be returned
</aside>

## Get All Quote Request
Coming Soon

## Get a Specific Quote Request
Coming Soon

#Port Object
##Model Parameters
Parameter | Type | Description
--------- | ------- | -----------
id | String | id of the port as stored in network microservice
name | String | name of the Port
iata_code | String |  3 character IATA Code for Airports
unloc_code | String | 5 character code for Locations defined by United Nations

#Address Object
##Model Parameters
Parameter | Type | Description
--------- | ------- | -----------
id | String | id of the address as stored in network microservice
name | String | Short name of the Address
address_type | String | Address Type
address_line_1 | String |  3 character IATA Code for Airports
address_line_2 | String | 5 character code for Locations defined by United Nations
city | String |
state | String |
country_code | String | 2 Character ISO country code
country | String | Country Name
postal_code | String | Pincode / Zip code of the area

#Collaborating Company Object
##Model Parameters
Parameter | Type | Description
--------- | ------- | -----------
quote_request_id | String | Id of quote request over which the company is collaborating (Not Required for quote request create call).
company_id | String | id of the company as stored in network microservice
name | String | Name of the company as stored in network
role | String | Role of the company on this quote request (buyer, seller)
