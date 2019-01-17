---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - json

toc_footers:
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to Diamond Foundry API! You can use our API to access product data, inventory data, and to place orders.

You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Authentication

JWT Token authentication is used.

To authenticate and get a token, hit the /login endpoint with your user credentials (email, password):

DF API expects for the JWT token to be included only in requests to Order endpoints:

`Authorization: Bearer meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal jwt-token key.
</aside>

## Login /login
/login authenticates user, response body contains a success message and response headers include authorization token.

```shell
curl -H "Content-Type: application/json" \
  --request POST \
  --data '{"email":"youremail@example.com","password":"password"}' \
  -k \
  https://dfoundry-diamonds.herokaupp.com/login
```

> Request body:

```json
{
	"email": "youremail@example.com",
	"password": "password"
}
```

> Note: successful authentication will include Authorization header in response headers. Response body is structured as so:

```json
{
  "message": "Authentication successful. JWT token included in this response."
}
```

# Diamond Endpoints

## /api/v1/diamonds

This endpoint retrieves all purchasable diamonds (available in US) with carat weight above 0.84.

### HTTP Request

`GET https://dfoundry-diamonds.herokuapp.com/api/v1/diamonds`

> Response body is structured like this:

```json
[
  {
    "carat": 1.18,
    "clarity": "SI2",
    "color": "J",
    "crown_angle": 35.0,
    "crown_height": 15.0,
    "cut_grade": "Ideal",
    "depth_mm": 4.21,
    "depth_pct": 61.6,
    "fluorescence": "None",
    "gcal_cert_id": null,
    "girdle": "Medium to Slightly Thick",
    "id": "61ab3229-168d-40b3-b38e-5199665cadb0",
    "length_mm": 6.81,
    "lot_id": 122049,
    "netsuite_id": 15724,
    "ns_location": "Los Angeles",
    "pavilion_angle": 40.8,
    "pavilion_height": 43.0,
    "polish": "Excellent",
    "quantity": 1,
    "shape": "Brilliant Round",
    "symmetry": "Excellent",
    "table_size": 57.0,
    "unit_price_msrp_usd": "2549.0"
  },
  {
    "carat": 1.12,
    "clarity": "VS1",
    "color": "I",
    "crown_angle": 34.0,
    "crown_height": 14.5,
    "cut_grade": "Ideal",
    "depth_mm": 4.11,
    "depth_pct": 61.3,
    "fluorescence": "None",
    "gcal_cert_id": 281060048,
    "girdle": "Medium to Slightly Thick",
    "id": "4aa1c735-a3da-478d-8e2e-f9c7f83269c7",
    "length_mm": 6.67,
    "lot_id": 147758,
    "netsuite_id": 17530,
    "ns_location": "Los Angeles",
    "pavilion_angle": 41.0,
    "pavilion_height": 43.5,
    "polish": "Excellent",
    "quantity": 1,
    "shape": "Brilliant Round",
    "symmetry": "Excellent",
    "table_size": 57.0,
    "unit_price_msrp_usd": "3427.0"
  }
]
```

```shell
curl 'https://dfoundry-diamonds.herokuapp.com/api/v1/diamonds'
```

## /api/v1/diamonds/{lot_id}

### HTTP Request

`GET https://dfoundry-diamonds.herokuapp.com/api/v1/diamonds/{lot_id}`

### URL Parameters

Parameter | Description
--------- | -----------
lot_id | The lot_id of the diamond to retrieve

> The endpoint returns JSON structured like this:

```json
{
  "carat": 1.18,
  "clarity": "SI2",
  "color": "J",
  "crown_angle": 35.0,
  "crown_height": 15.0,
  "cut_grade": "Ideal",
  "depth_mm": 4.21,
  "depth_pct": 61.6,
  "fluorescence": "None",
  "gcal_cert_id": null,
  "girdle": "Medium to Slightly Thick",
  "id": "61ab3229-168d-40b3-b38e-5199665cadb0",
  "length_mm": 6.81,
  "lot_id": 122049,
  "netsuite_id": 15724,
  "ns_location": "Los Angeles",
  "pavilion_angle": 40.8,
  "pavilion_height": 43.0,
  "polish": "Excellent",
  "quantity": 1,
  "shape": "Brilliant Round",
  "symmetry": "Excellent",
  "table_size": 57.0,
  "unit_price_msrp_usd": "2549.0"
}
```

```shell
curl 'https://dfoundry-diamonds.herokuapp.com/api/v1/diamonds/122049'
```

This endpoint retrieves a specific diamond.


# Order Endpoints

## Create an order

### HTTP Request

`POST https://dfoundry-diamonds.herokuapp.com/api/v1/orders`

### Request body 

> Request body must be structured like this: 

```json
{
  "order":  
	  {
			"source_order_id": 781449461863,
			"payment_method": "net30",
			"shipping_address_attributes":  
				{
					"street_address": "731 S Spring St",
					"city": "Los Angeles",
					"country": "United States",
					"state": "California",
					"name": "Alex Szabo"
				},
			"order_items_attributes":  
				[{
					"diamond_id": "c41a93db-2b6a-4ffe-95e0-fa24b0d3f3d6",
					"sold_price": 500.45,
					"tax_collected": "36.28",
					"tax_rate": 0.0725,
					"quantity": 1
				}]
    }
}
```

## Order Parameters

Parameter | Description | Type | Required
--------- | ----------- | ---- | --------
source_order_id | The order ID on the platform where the order was placed | int | required
payment_method | Method used to pay for order | string | required
metadata | Additional metadata about the order | jsonb | optional

## Nested shipping_address_attributes

Parameter | Description | Type | Required
--------- | ----------- | ---- | --------
street_address | Address to send order | string | required
city | | string | required
state | state/province of order | string | required
country | country to send order (ex: 'USA') | string | required
zip | zip code | string | not required 
name | name of addressee/recipient | string | not required
phone | phone number of recipient | string | not required
attention | | string | not required

## Nested order_items_attributes

Parameter | Description | Type | Required
--------- | ----------- | ---- | --------
diamond_id | DF API diamond id | uuid/string | required
sold_price | Amount diamond sold for | decimal | required
tax_collected | Tax collected on diamond | decimal | optional
tax_rate | Sales tax rate pct of where sale occurred (ex 0.0125) | decimal | optional
quantity | Quantity sold | integer | required
