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
  https://rest.diamondfoundry.com/login
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

`GET https://rest.diamondfoundry.com/api/v1/diamonds`

> Response body is structured like this:

```json
[
  {
    "carat": 1.55,
    "clarity": "VS1",
    "color": "H",
    "created_at": "2018-12-20T00:04:35.310Z",
    "crown_angle": 35.8,
    "crown_height": 13.9,
    "cut_grade": "Ideal",
    "depth_mm": 3.88,
    "depth_pct": 59.1,
    "fluorescence": "None",
    "gcal_cert_id": 280850143,
    "girdle": "Slightly Thick",
    "id": "f1bd82a3-5ff3-47fb-9955-5ebef91fe3b9",
    "length_mm": 9.03,
    "lot_id": 130867,
    "netsuite_id": 17791,
    "ns_location": "Los Angeles",
    "pavilion_angle": 38.8,
    "pavilion_height": 40.1,
    "polish": "Excellent",
    "quantity": 1,
    "shape": "Oval",
    "symmetry": "Excellent",
    "table_size": 60.3,
    "unit_price_msrp_usd": "6456.0",
    "updated_at": "2019-02-06T15:06:32.457Z",
    "width_mm": 6.53
  },
  {
    "carat": 1.01,
    "clarity": "SI1",
    "color": "H",
    "created_at": "2018-12-20T00:05:42.251Z",
    "crown_angle": 38.0,
    "crown_height": 14.8,
    "cut_grade": "Very Good",
    "depth_mm": 3.43,
    "depth_pct": 61.0,
    "fluorescence": "None",
    "gcal_cert_id": null,
    "girdle": "Very Thick",
    "id": "75c6d9a6-2710-4f6f-b571-8154ef3bb024",
    "length_mm": 7.74,
    "lot_id": 72737,
    "netsuite_id": 4796,
    "ns_location": "Los Angeles",
    "pavilion_angle": 38.9,
    "pavilion_height": 40.0,
    "polish": "Excellent",
    "quantity": 1,
    "shape": "Oval",
    "symmetry": "Very Good",
    "table_size": 62.7,
    "unit_price_msrp_usd": "3091.0",
    "updated_at": "2019-02-06T14:33:14.021Z",
    "width_mm": 5.62
  },
  {
    "carat": 1.09,
    "clarity": "VS1",
    "color": "G",
    "created_at": "2019-01-04T23:33:39.458Z",
    "crown_angle": 35.7,
    "crown_height": 13.7,
    "cut_grade": "Excellent",
    "depth_mm": 3.48,
    "depth_pct": 58.8,
    "fluorescence": "None",
    "gcal_cert_id": 283480036,
    "girdle": "Thin to Slightly Thick",
    "id": "87b0f288-41ee-4c18-9a5a-d252a7b85405",
    "length_mm": 8.21,
    "lot_id": 202232,
    "netsuite_id": 106280,
    "ns_location": "Los Angeles",
    "pavilion_angle": 38.8,
    "pavilion_height": 41.2,
    "polish": "Very Good",
    "quantity": 1,
    "shape": "Oval",
    "symmetry": "Very Good",
    "table_size": 58.0,
    "unit_price_msrp_usd": "4415.0",
    "updated_at": "2019-02-06T14:45:16.028Z",
    "width_mm": 5.92
  },
  {
    "carat": 1.02,
    "clarity": "VS1",
    "color": "G",
    "created_at": "2019-01-04T23:33:39.376Z",
    "crown_angle": 35.2,
    "crown_height": 14.7,
    "cut_grade": "Excellent",
    "depth_mm": 3.51,
    "depth_pct": 62.0,
    "fluorescence": "None",
    "gcal_cert_id": 283480032,
    "girdle": "Medium to Thick",
    "id": "6d877f36-8ac8-4ffb-bdf1-0b848abf4cbc",
    "length_mm": 8.0,
    "lot_id": 202445,
    "netsuite_id": 106272,
    "ns_location": "Los Angeles",
    "pavilion_angle": 39.9,
    "pavilion_height": 42.9,
    "polish": "Very Good",
    "quantity": 1,
    "shape": "Oval",
    "symmetry": "Very Good",
    "table_size": 55.0,
    "unit_price_msrp_usd": "4131.0",
    "updated_at": "2019-02-06T14:32:48.474Z",
    "width_mm": 5.66
  }
]
```

```shell
curl 'https://rest.diamondfoundry.com/api/v1/diamonds'
```

## /api/v1/diamonds query string params
/api/v1/diamonds takes optional query string params in array form for attributes 'shape', 'color', 'cut_grade', and 'clarity'. /api/v1/diamonds also takes 'extended' query string param which optionally nests digital assets within the diamond (for those diamonds that have digital assets associated to it):

### HTTP Request w/ query string params (without extended)
`GET https://rest.diamondfoundry.com/api/v1/diamonds?shape[]=oval&shape[]=pear&color[]=d&color[]=f&color[]=g&color[]=h`

```json
[
  {
    "carat": 1.55,
    "clarity": "VS1",
    "color": "H",
    "created_at": "2018-12-20T00:04:35.310Z",
    "crown_angle": 35.8,
    "crown_height": 13.9,
    "cut_grade": "Ideal",
    "depth_mm": 3.88,
    "depth_pct": 59.1,
    "fluorescence": "None",
    "gcal_cert_id": 280850143,
    "girdle": "Slightly Thick",
    "id": "f1bd82a3-5ff3-47fb-9955-5ebef91fe3b9",
    "length_mm": 9.03,
    "lot_id": 130867,
    "netsuite_id": 17791,
    "ns_location": "Los Angeles",
    "pavilion_angle": 38.8,
    "pavilion_height": 40.1,
    "polish": "Excellent",
    "quantity": 1,
    "shape": "Oval",
    "symmetry": "Excellent",
    "table_size": 60.3,
    "unit_price_msrp_usd": "6456.0",
    "updated_at": "2019-02-06T15:06:32.457Z",
    "width_mm": 6.53
  },
  {
    "carat": 1.01,
    "clarity": "SI1",
    "color": "H",
    "created_at": "2018-12-20T00:05:42.251Z",
    "crown_angle": 38.0,
    "crown_height": 14.8,
    "cut_grade": "Very Good",
    "depth_mm": 3.43,
    "depth_pct": 61.0,
    "fluorescence": "None",
    "gcal_cert_id": null,
    "girdle": "Very Thick",
    "id": "75c6d9a6-2710-4f6f-b571-8154ef3bb024",
    "length_mm": 7.74,
    "lot_id": 72737,
    "netsuite_id": 4796,
    "ns_location": "Los Angeles",
    "pavilion_angle": 38.9,
    "pavilion_height": 40.0,
    "polish": "Excellent",
    "quantity": 1,
    "shape": "Oval",
    "symmetry": "Very Good",
    "table_size": 62.7,
    "unit_price_msrp_usd": "3091.0",
    "updated_at": "2019-02-06T14:33:14.021Z",
    "width_mm": 5.62
  },
  {
    "carat": 1.09,
    "clarity": "VS1",
    "color": "G",
    "created_at": "2019-01-04T23:33:39.458Z",
    "crown_angle": 35.7,
    "crown_height": 13.7,
    "cut_grade": "Excellent",
    "depth_mm": 3.48,
    "depth_pct": 58.8,
    "fluorescence": "None",
    "gcal_cert_id": 283480036,
    "girdle": "Thin to Slightly Thick",
    "id": "87b0f288-41ee-4c18-9a5a-d252a7b85405",
    "length_mm": 8.21,
    "lot_id": 202232,
    "netsuite_id": 106280,
    "ns_location": "Los Angeles",
    "pavilion_angle": 38.8,
    "pavilion_height": 41.2,
    "polish": "Very Good",
    "quantity": 1,
    "shape": "Oval",
    "symmetry": "Very Good",
    "table_size": 58.0,
    "unit_price_msrp_usd": "4415.0",
    "updated_at": "2019-02-06T14:45:16.028Z",
    "width_mm": 5.92
  },
  {
    "carat": 1.02,
    "clarity": "VS1",
    "color": "G",
    "created_at": "2019-01-04T23:33:39.376Z",
    "crown_angle": 35.2,
    "crown_height": 14.7,
    "cut_grade": "Excellent",
    "depth_mm": 3.51,
    "depth_pct": 62.0,
    "fluorescence": "None",
    "gcal_cert_id": 283480032,
    "girdle": "Medium to Thick",
    "id": "6d877f36-8ac8-4ffb-bdf1-0b848abf4cbc",
    "length_mm": 8.0,
    "lot_id": 202445,
    "netsuite_id": 106272,
    "ns_location": "Los Angeles",
    "pavilion_angle": 39.9,
    "pavilion_height": 42.9,
    "polish": "Very Good",
    "quantity": 1,
    "shape": "Oval",
    "symmetry": "Very Good",
    "table_size": 55.0,
    "unit_price_msrp_usd": "4131.0",
    "updated_at": "2019-02-06T14:32:48.474Z",
    "width_mm": 5.66
  }
]
```

## /api/v1/diamonds?extended=t with 'extended' query string param

### HTTP Request w/ query string params (with 'extended')

```json
[
  {
    "carat": 1.18,
    "clarity": "SI1",
    "color": "J",
    "created_at": "2019-01-21T23:05:10.164Z",
    "crown_angle": 34.0,
    "crown_height": 14.0,
    "cut_grade": "Ideal",
    "depth_mm": 4.14,
    "depth_pct": 60.6,
    "digital_assets": [
      {
        "kind": "video",
        "url": "https://s3.amazonaws.com/videos.diamondfoundry.com/203715.mp4"
      }
    ],
    "fluorescence": "None",
    "gcal_cert_id": 290040043,
    "girdle": "Medium to Slightly Thick",
    "id": "9f6973f6-de78-46af-adc7-950939361ae9",
    "length_mm": 6.81,
    "lot_id": 203715,
    "netsuite_id": 108282,
    "ns_location": "Los Angeles",
    "pavilion_angle": 41.0,
    "pavilion_height": 43.5,
    "polish": "Excellent",
    "quantity": 1,
    "shape": "Brilliant Round",
    "symmetry": "Excellent",
    "table_size": 59.0,
    "unit_price_msrp_usd": "2814.0",
    "updated_at": "2019-02-06T14:56:44.882Z",
    "width_mm": 6.85
  },
  {
    "carat": 1.61,
    "clarity": "VS1",
    "color": "I",
    "created_at": "2018-12-20T00:05:53.056Z",
    "crown_angle": 0.0,
    "crown_height": 10.6,
    "cut_grade": "Excellent",
    "depth_mm": 4.53,
    "depth_pct": 71.6,
    "digital_assets": [],
    "fluorescence": "None",
    "gcal_cert_id": 281730085,
    "girdle": "Thin to Slightly Thick",
    "id": "884eb54c-e2e1-4c15-be7b-f686c3a46ab0",
    "length_mm": 6.48,
    "lot_id": 174939,
    "netsuite_id": 49986,
    "ns_location": "Los Angeles",
    "pavilion_angle": 0.0,
    "pavilion_height": 58.0,
    "polish": "Very Good",
    "quantity": 1,
    "shape": "Princess",
    "symmetry": "Very Good",
    "table_size": 70.0,
    "unit_price_msrp_usd": "5611.0",
    "updated_at": "2019-02-06T15:26:59.130Z",
    "width_mm": 6.33
  }
]
```

## /api/v1/diamonds/{lot_id}

### HTTP Request

`GET https://rest.diamondfoundry.com/api/v1/diamonds/{lot_id}`

### URL Parameters

Parameter | Description
--------- | -----------
lot_id | The lot_id of the diamond to retrieve

> The endpoint returns JSON structured like this:

```json
{
  "carat": 1.61,
  "clarity": "VS1",
  "color": "I",
  "created_at": "2018-12-20T00:05:53.056Z",
  "crown_angle": 0.0,
  "crown_height": 10.6,
  "cut_grade": "Excellent",
  "depth_mm": 4.53,
  "depth_pct": 71.6,
  "digital_assets": [],
  "fluorescence": "None",
  "gcal_cert_id": 281730085,
  "girdle": "Thin to Slightly Thick",
  "id": "884eb54c-e2e1-4c15-be7b-f686c3a46ab0",
  "length_mm": 6.48,
  "lot_id": 174939,
  "netsuite_id": 49986,
  "ns_location": "Los Angeles",
  "pavilion_angle": 0.0,
  "pavilion_height": 58.0,
  "polish": "Very Good",
  "quantity": 1,
  "shape": "Princess",
  "symmetry": "Very Good",
  "table_size": 70.0,
  "unit_price_msrp_usd": "5611.0",
  "updated_at": "2019-02-06T15:26:59.130Z",
  "width_mm": 6.33
}
```

```shell
curl 'https://rest.diamondfoundry.com/api/v1/diamonds/122049'
```

This endpoint retrieves a specific diamond.


# Order Endpoints

## Create Order 

### POST /api/v1/orders

### HTTP Request

`POST https://rest.diamondfoundry.com/api/v1/orders`

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
payment_method | Method used to pay for order | string | optional
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

## GET /api/v1/orders

### HTTP Request

`GET https://rest.diamondfoundry.com/api/v1/orders`

> Must include JWT-token eg: ```Authorization: Bearer erwevcfwegfwegrweg``` in request headers.

> Response JSON is structured like this: 

```json
[
  {
    "created_by_id": "252e5207-3a31-4995-b5c3-20fb31bc9805",
    "erp_id": null,
    "id": "fb074590-41de-461b-bc10-fbb2a35cb652",
    "order_items": [
      {
        "diamond_id": "c41a93db-2b6a-4ffe-95e0-fa24b0d3f3d6",
        "price_extended": "2841.0",
        "quantity": 1,
        "sold_price": "500.45",
        "tax_collected": "36.28",
        "tax_rate": "0.0725"
      }
    ],
    "payment_method": "manual",
    "shipping_address": {
      "attention": null,
      "city": "Santa Monica",
      "country": "United States",
      "line_2": null,
      "line_3": null,
      "phone": null,
      "state": "CA",
      "street_address": "2512 Michigan Ave",
      "zip": null
    },
    "source_order_id": 781449461862
  },
  {
    "created_by_id": "252e5207-3a31-4995-b5c3-20fb31bc9805",
    "erp_id": null,
    "id": "8bbef1ef-cda0-481d-b10d-5d3fef48e062",
    "order_items": [
      {
        "diamond_id": "c41a93db-2b6a-4ffe-95e0-fa24b0d3f3d6",
        "price_extended": "2841.0",
        "quantity": 1,
        "sold_price": "500.45",
        "tax_collected": "36.28",
        "tax_rate": "0.0725"
      }
    ],
    "payment_method": "net30",
    "shipping_address": {
      "attention": null,
      "city": "Los Angeles",
      "country": "United States",
      "line_2": null,
      "line_3": null,
      "phone": null,
      "state": "California",
      "street_address": "731 S Spring St",
      "zip": null
    },
    "source_order_id": 781449461863
  }
]
```

## GET Specific Order

## /api/v1/orders/{id}

### HTTP Request

`GET https://rest.diamondfoundry.com/api/v1/orders/fb074590-41de-461b-bc10-fbb2a35cb652`

> Again must include JWT-token in request headers ex: ```Authorization: Bearer erwevcfwegfwegrweg```.

```json
{
  "created_by_id": "252e5207-3a31-4995-b5c3-20fb31bc9805",
  "erp_id": null,
  "id": "fb074590-41de-461b-bc10-fbb2a35cb652",
  "order_items": [
    {
      "diamond_id": "c41a93db-2b6a-4ffe-95e0-fa24b0d3f3d6",
      "price_extended": "2841.0",
      "quantity": 1,
      "sold_price": "500.45",
      "tax_collected": "36.28",
      "tax_rate": "0.0725"
    }
  ],
  "payment_method": "manual",
  "shipping_address": {
    "attention": null,
    "city": "Santa Monica",
    "country": "United States",
    "line_2": null,
    "line_3": null,
    "phone": null,
    "state": "CA",
    "street_address": "2512 Michigan Ave",
    "zip": null
  },
  "source_order_id": 781449461862
}
```

# User Registration

## Create User

### POST /api/v1/register

`POST https://rest.diamondfoundry.com/api/v1/register`

### Request body 

> Request body must be structured like this: 

```json
{
  "user": {
		"email": "herbie@example.com",
		"first_name": "Herbie",
		"last_name": "Hancock",
		"phone": "9782235621",
		"company_name": "Jazz Co.",
		"password": "4gX2Tq&zFBxYVh"
	}
}
```

## User Create Parameters

Parameter | Description | Type | Required
--------- | ----------- | ---- | --------
email | your email address | string | required
first_name | your first name | string | optional
last_name | your last name | string | optional
company_name | your businesses name | string | optional
phone | number you can be reached at | string | optional

## Update User

### PUT/PATCH /api/v1/register

`PUT https://rest.diamondfoundry.com/api/v1/register`

### Request body 

Please note valid Authorization header with JWT Token is required.

current_password parameter is also required to update resource.

> Request body must be structured like this: 

```json
{
  "user": {
		"email": "herbie@example.com",
		"first_name": "Herbie",
		"last_name": "Hancock JR",
		"phone": "9782235621",
		"company_name": "Herbie Jazz Inc.",
		"current_password": "4gX2Tq&zFBxYVh"
	}
}
```
Parameter | Description | Type | Required
--------- | ----------- | ---- | --------
current_password | your current password | string | required 

### Response body

> Response JSON is structured like this: 

```json
{
  "company_name": "Herbie Jazz Inc.",
  "email": "herbie@example.com",
  "first_name": "Herbie",
  "last_name": "Hancock JR",
  "phone": "9782235621",
  "status": null
}
```

## Get User

### GET /api/v1/user

`GET https://rest.diamondfoundry.com/api/v1/user`

Please note valid Authorization header with JWT Token is required.

### Response body 

> Response JSON is structured like this: 

```json
{
  "company_name": "Herbie Jazz Inc.",
  "email": "herbie@example.com",
  "first_name": "Herbie",
  "last_name": "Hancock JR",
  "phone": "9782235621",
  "status": null
}
```