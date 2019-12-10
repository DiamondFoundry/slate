---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to Diamond Foundry API! You can use our API to access diamond inventory and place orders.

# Authentication

## JWT Token Authentication

You can authorize by providing your JWT token in the header of the request.

`Authorization: Bearer meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal jwt-token key.
</aside>

To obtain a JWT token, you must log in using your username and password.

### Login /login

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

> The response headers will include the Authorization header.

```json
{
  "Authorization": "Bearer THISISYOURTOKEN"
}
```

## API Key Authentication

You can also authorize using your API Key. To get your API key, you must go to your dashboard on the B2B Portal.

Log in here: https://portal.diamondfoundry.com/login

Then click the three-lines (hamburger) menu in the upper right corner of the screen. Then click on "Dashboard".

Your API Key should be displayed in a panel on the lower portion of the screen.

You can then use that by adding it onto your API requests, along with your email address: `GET https://rest.diamondfoundry.com/api/v2/diamonds?user_email=your@email.com&user_token=YOUR_TOKEN` 

REMINDER: Always send requests to HTTPS endpoints, or else you are exposing your API key to anyone who is watching.

```shell
curl -H "Content-Type: application/json" \
  --request GET \
  -k \
  https://rest.diamondfoundry.com/api/v2/diamonds?user_email=your@email.com&user_token=YOUR_TOKEN
```

# V1 Diamond endpoints

## /api/v1/diamonds

This endpoint retrieves all purchasable diamonds (available in US) with carat weight above 0.84. 

Differences between this endpoint and /api/v2/diamonds: 

1. /api/v2/diamonds requires authentication
2. /api/v1/diamonds includes only diamonds above 0.84 carats
3. /api/v1/diamonds includes MSRP pricing only.
4. /api/v2/diamonds includes both MSRP price and account discount/wholesale price.
5. /api/v1/diamonds allows query params to scope the response type. Please see more info and details listed below for each query param.

For account specific pricing you must authenticate and use v2 diamonds.

**Certificates**

Diamond Foundry has a pdf certificate accessible for diamonds. In order to access it use the following path and interpolate the `lot_id` of the diamond: 
`https://certificate.diamondfoundry.com/download/${lot_id}.pdf` 

example: `https://certificate.diamondfoundry.com/download/169610.pdf`

169610 is the lot id.

**Videos**

Links to videos are optionally accessible using query string param 'extended' in the /api/v1/diamonds endpoint. They are nested by default in the /api/v2/diamonds endpoint. Not all diamonds have videos.

For videos, the `url` key is a link to the mp3 file. For more info view the individual endpoint documentation.

### HTTP Request

`GET https://rest.diamondfoundry.com/api/v1/diamonds`

```shell
curl 'https://rest.diamondfoundry.com/api/v1/diamonds'
```

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

## /api/v1/diamonds query string params
/api/v1/diamonds takes optional query string params in array form for attributes 'shape', 'color', 'cut_grade', and 'clarity'. /api/v1/diamonds also takes 'extended' query string param which optionally nests digital assets within the diamond (for those diamonds that have digital assets associated to it):

* Please note; to include digital assets (eg links to video files) you must include the `extended` query param. See how to do that below.

Also, please note that the url is a link to a video.

See the difference in response bodies below.

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

* Please note that the url is a link to a video.

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
        "url": "https://videos.diamondfoundry.com/203715.mp4"
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
			"payment_method": "B2B Stripe",
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
					"tax_rate": 0,
					"quantity": 1
				}]
    }
}
```

## Order Parameters

Parameter | Description | Type | Required
--------- | ----------- | ---- | --------
payment_method | Method used to pay for order. To pay with your credit card saved on the B2B Portal, use 'B2B Stripe'. To pay on lay away, if you are approved to do so, send the empty string, ''. | string | optional
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
tax_collected | Tax collected on diamond. Since this is a B2B sale, this should always be 0. | decimal | optional
tax_rate | Sales tax rate pct of where sale occurred (ex 0.0125). Since this is a B2B sale, this should always be 0. | decimal | optional
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
phone | number you can be reached at | string | optional
password | minimum length 6 | string | required

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
		"current_password": "4gX2Tq&zFBxYVh"
	}
}
```

Include any attributes you want to update

Parameter | Description | Type | Required
--------- | ----------- | ---- | --------
current_password | your current password | string | required 

### Response body

> Response JSON is structured like this: 

```json
{
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
  "email": "herbie@example.com",
  "first_name": "Herbie",
  "last_name": "Hancock JR",
  "phone": "9782235621",
  "status": null
}
```

# Reset User Password

## Request Password Reset Email
### POST /api/v1/users/password

`POST https://rest.diamondfoundry.com/api/v1/users/password`

Sends User Password Reset email

> Request body must be structured like this: 

```json
{
	"user": {
		"email": "herbie.hancock@example.com"
	}
}
```

> Response will be empty body with status code 202 for successful requests

## Reset: Set new password
### PUT/PATCH /api/v1/users/password

`PATCH https://rest.diamondfoundry.com/api/v1/users/password`

> Request body must be structured like this note* inclusion of reset_password_token which is query param in url sent via email: 

```json
{
	"user": {
		"email": "herbie.hancock@example.com",
		"password": "my_new_password",
		"reset_password_token": "R63tfseV1eBB7x-zyAG5"
	}
}
```

> Response will be empty body with status code 200 for successful requests

# V2 Diamond Endpoints

## /api/v2/diamonds

`GET https://rest.diamondfoundry.com/api/v2/diamonds`

This endpoint fetches available diamonds >= 0.3 carats.

Please note valid Authorization header with JWT Token or API Key is required. See [login documentation](#login-login).

/api/v2/diamonds includes both MSRP price and account discount/wholesale price.

The ```prices``` array contains your account's wholesale/discount price.

Keys | Description | Type
--------- | ----------- | ---- 
unit_price_msrp_usd | MSRP suggested retail price | string
amount_usd | 'amount_usd' (nested in the prices array) is the wholesale/discount price. This is the price your account will be charged. | string


### Authorization header

> The request header should be formatted like this.

```json
{
  "Content-Type": "application/json", 
  "Authorization": "Bearer YOURTOKENGOESHERE"
}
```

### Response body 

> Response JSON is structured like this: 

```json
[
  {
    "carat": 1.65,
    "clarity": "VS2",
    "color": "J",
    "created_at": "2019-05-13T18:29:27.190Z",
    "crown_angle": 35.3,
    "crown_height": 13.4,
    "cut_grade": "Excellent",
    "depth_mm": 3.77,
    "depth_pct": 62.4,
    "digital_assets": [],
    "fluorescence": "None",
    "gcal_cert_id": null,
    "girdle": "Slightly Thick",
    "id": "64de1a90-3dab-4442-b457-ded4bc387b18",
    "length_mm": 8.17,
    "lot_id": 122616,
    "netsuite_id": 15743,
    "ns_location": "Los Angeles",
    "pavilion_angle": 42.0,
    "pavilion_height": 44.9,
    "polish": "Excellent",
    "prices": [
      {
        "amount_usd": "2777.0",
        "name": "MSRP-40%"
      }
    ],
    "quantity": 1,
    "shape": "Emerald",
    "symmetry": "Excellent",
    "table_size": 61.5,
    "unit_price_msrp_usd": "4628.0",
    "updated_at": "2019-05-20T18:44:28.384Z",
    "width_mm": 6.04
  },
  {
    "carat": 1.15,
    "clarity": "VS1",
    "color": "I",
    "created_at": "2019-05-13T18:29:27.211Z",
    "crown_angle": 34.5,
    "crown_height": 15.0,
    "cut_grade": "Ideal",
    "depth_mm": 4.16,
    "depth_pct": 61.5,
    "digital_assets": [],
    "fluorescence": "None",
    "gcal_cert_id": null,
    "girdle": "Medium",
    "id": "dce507f1-9f43-480e-a5d4-b608aa070db6",
    "length_mm": 6.78,
    "lot_id": 122749,
    "netsuite_id": 15766,
    "ns_location": "Los Angeles",
    "pavilion_angle": 40.8,
    "pavilion_height": 43.0,
    "polish": "Excellent",
    "prices": [
      {
        "amount_usd": "2111.0",
        "name": "MSRP-40%"
      }
    ],
    "quantity": 1,
    "shape": "Brilliant Round",
    "symmetry": "Excellent",
    "table_size": 56.0,
    "unit_price_msrp_usd": "3519.0",
    "updated_at": "2019-05-20T18:44:28.392Z",
    "width_mm": 6.74
  },
  {
    "carat": 1.59,
    "clarity": "SI2",
    "color": "J",
    "created_at": "2019-05-13T18:29:27.290Z",
    "crown_angle": 0.0,
    "crown_height": 14.9,
    "cut_grade": "Excellent",
    "depth_mm": 3.69,
    "depth_pct": 63.0,
    "digital_assets": [],
    "fluorescence": "None",
    "gcal_cert_id": 280640136,
    "girdle": "Medium",
    "id": "c96969f6-bb69-4f8e-851f-8281b195c39f",
    "length_mm": 8.09,
    "lot_id": 129033,
    "netsuite_id": 16377,
    "ns_location": "Los Angeles",
    "pavilion_angle": 0.0,
    "pavilion_height": 45.7,
    "polish": "Excellent",
    "prices": [
      {
        "amount_usd": "2271.0",
        "name": "MSRP-40%"
      }
    ],
    "quantity": 1,
    "shape": "Emerald",
    "symmetry": "Excellent",
    "table_size": 60.8,
    "unit_price_msrp_usd": "3784.0",
    "updated_at": "2019-05-20T18:44:28.524Z",
    "width_mm": 5.82
  },
  {
    "carat": 0.96,
    "clarity": "VS1",
    "color": "I",
    "created_at": "2019-05-13T18:29:27.294Z",
    "crown_angle": 0.0,
    "crown_height": 14.0,
    "cut_grade": "Ideal",
    "depth_mm": 3.1,
    "depth_pct": 62.4,
    "digital_assets": [],
    "fluorescence": "None",
    "gcal_cert_id": 280640108,
    "girdle": "Medium",
    "id": "7cc8b163-4f2c-4feb-9965-33ec5b146b8c",
    "length_mm": 6.95,
    "lot_id": 129754,
    "netsuite_id": 16458,
    "ns_location": "Los Angeles",
    "pavilion_angle": 0.0,
    "pavilion_height": 45.6,
    "polish": "Excellent",
    "prices": [
      {
        "amount_usd": "1400.0",
        "name": "MSRP-40%"
      }
    ],
    "quantity": 1,
    "shape": "Emerald",
    "symmetry": "Excellent",
    "table_size": 61.6,
    "unit_price_msrp_usd": "2333.0",
    "updated_at": "2019-05-20T18:44:28.530Z",
    "width_mm": 4.93
  },
  {
    "carat": 1.26,
    "clarity": "VS2",
    "color": "K",
    "created_at": "2019-05-13T18:29:27.343Z",
    "crown_angle": 32.7,
    "crown_height": 11.7,
    "cut_grade": "Ideal",
    "depth_mm": 2.76,
    "depth_pct": 44.8,
    "digital_assets": [],
    "fluorescence": "None",
    "gcal_cert_id": null,
    "girdle": "Very Thick",
    "id": "330d54a5-da22-46ff-9743-753826e8e126",
    "length_mm": 8.37,
    "lot_id": 113522,
    "netsuite_id": 15111,
    "ns_location": "Los Angeles",
    "pavilion_angle": 15.0,
    "pavilion_height": 26.1,
    "polish": "Excellent",
    "prices": [
      {
        "amount_usd": "1531.0",
        "name": "MSRP-40%"
      }
    ],
    "quantity": 1,
    "shape": "Oval Rose",
    "symmetry": "Excellent",
    "table_size": 64.0,
    "unit_price_msrp_usd": "2552.0",
    "updated_at": "2019-05-20T18:44:28.594Z",
    "width_mm": 6.16
  },
  {
    "carat": 1.14,
    "clarity": "VS1",
    "color": "I",
    "created_at": "2019-05-13T18:29:27.325Z",
    "crown_angle": 34.5,
    "crown_height": 14.5,
    "cut_grade": "Ideal",
    "depth_mm": 4.14,
    "depth_pct": 61.6,
    "digital_assets": [],
    "fluorescence": "None",
    "gcal_cert_id": 280710031,
    "girdle": "Medium to Slightly Thick",
    "id": "a73f6328-f2e2-43ac-ba94-27cf6e9e7fcc",
    "length_mm": 6.71,
    "lot_id": 134009,
    "netsuite_id": 16539,
    "ns_location": "Los Angeles",
    "pavilion_angle": 40.8,
    "pavilion_height": 43.0,
    "polish": "Excellent",
    "prices": [
      {
        "amount_usd": "2093.0",
        "name": "MSRP-40%"
      }
    ],
    "quantity": 1,
    "shape": "Brilliant Round",
    "symmetry": "Excellent",
    "table_size": 57.0,
    "unit_price_msrp_usd": "3488.0",
    "updated_at": "2019-05-20T18:44:28.572Z",
    "width_mm": 6.73
  },
  {
    "carat": 1.17,
    "clarity": "VS1",
    "color": "I",
    "created_at": "2019-05-13T18:29:27.467Z",
    "crown_angle": 34.5,
    "crown_height": 15.0,
    "cut_grade": "Ideal",
    "depth_mm": 4.19,
    "depth_pct": 61.6,
    "digital_assets": [],
    "fluorescence": "None",
    "gcal_cert_id": 280640044,
    "girdle": "Thin to Medium",
    "id": "7157b32a-cdbf-4cca-ad7a-edb8d914e1bc",
    "length_mm": 6.79,
    "lot_id": 127633,
    "netsuite_id": 16234,
    "ns_location": "Los Angeles",
    "pavilion_angle": 41.0,
    "pavilion_height": 43.5,
    "polish": "Excellent",
    "prices": [
      {
        "amount_usd": "2148.0",
        "name": "MSRP-40%"
      }
    ],
    "quantity": 1,
    "shape": "Brilliant Round",
    "symmetry": "Excellent",
    "table_size": 56.0,
    "unit_price_msrp_usd": "3580.0",
    "updated_at": "2019-05-20T18:44:28.720Z",
    "width_mm": 6.82
  },
  {
    "carat": 1.18,
    "clarity": "VS2",
    "color": "I",
    "created_at": "2019-05-13T18:29:27.412Z",
    "crown_angle": 35.0,
    "crown_height": 15.0,
    "cut_grade": "Ideal",
    "depth_mm": 4.21,
    "depth_pct": 61.9,
    "digital_assets": [],
    "fluorescence": "None",
    "gcal_cert_id": null,
    "girdle": "Medium to Slightly Thick",
    "id": "7eea3723-9719-4e8e-8e29-6b35ce68a790",
    "length_mm": 6.8,
    "lot_id": 125549,
    "netsuite_id": 16018,
    "ns_location": "Los Angeles",
    "pavilion_angle": 41.0,
    "pavilion_height": 43.5,
    "polish": "Excellent",
    "prices": [
      {
        "amount_usd": "2103.0",
        "name": "MSRP-40%"
      }
    ],
    "quantity": 1,
    "shape": "Brilliant Round",
    "symmetry": "Excellent",
    "table_size": 57.0,
    "unit_price_msrp_usd": "3505.0",
    "updated_at": "2019-05-20T18:44:28.669Z",
    "width_mm": 6.77
  },
  {
    "carat": 1.13,
    "clarity": "VS2",
    "color": "I",
    "created_at": "2019-05-13T18:29:27.563Z",
    "crown_angle": 34.5,
    "crown_height": 15.0,
    "cut_grade": "Ideal",
    "depth_mm": 4.14,
    "depth_pct": 61.7,
    "digital_assets": [],
    "fluorescence": "None",
    "gcal_cert_id": 280930024,
    "girdle": "Medium",
    "id": "8fcdacc2-df0f-4de9-ae52-bea07644e278",
    "length_mm": 6.7,
    "lot_id": 144576,
    "netsuite_id": 17548,
    "ns_location": "Los Angeles",
    "pavilion_angle": 41.0,
    "pavilion_height": 43.5,
    "polish": "Excellent",
    "prices": [
      {
        "amount_usd": "2014.0",
        "name": "MSRP-40%"
      }
    ],
    "quantity": 1,
    "shape": "Brilliant Round",
    "symmetry": "Excellent",
    "table_size": 57.0,
    "unit_price_msrp_usd": "3356.0",
    "updated_at": "2019-05-20T18:44:28.819Z",
    "width_mm": 6.71
  },
  {
    "carat": 1.14,
    "clarity": "VS1",
    "color": "J",
    "created_at": "2019-05-13T18:29:27.569Z",
    "crown_angle": 34.5,
    "crown_height": 15.0,
    "cut_grade": "Ideal",
    "depth_mm": 4.14,
    "depth_pct": 61.8,
    "digital_assets": [],
    "fluorescence": "None",
    "gcal_cert_id": 281000175,
    "girdle": "Medium to Slightly Thick",
    "id": "e3d591b8-ba9e-419c-b32f-96856d13f942",
    "length_mm": 6.69,
    "lot_id": 144704,
    "netsuite_id": 17550,
    "ns_location": "Los Angeles",
    "pavilion_angle": 41.0,
    "pavilion_height": 43.5,
    "polish": "Excellent",
    "prices": [
      {
        "amount_usd": "1816.0",
        "name": "MSRP-40%"
      }
    ],
    "quantity": 1,
    "shape": "Brilliant Round",
    "symmetry": "Excellent",
    "table_size": 57.0,
    "unit_price_msrp_usd": "3027.0",
    "updated_at": "2019-05-20T18:44:28.844Z",
    "width_mm": 6.71
  },
  {
    "carat": 1.14,
    "clarity": "VS1",
    "color": "J",
    "created_at": "2019-05-13T18:29:27.574Z",
    "crown_angle": 34.0,
    "crown_height": 14.5,
    "cut_grade": "Ideal",
    "depth_mm": 4.12,
    "depth_pct": 61.1,
    "digital_assets": [],
    "fluorescence": "None",
    "gcal_cert_id": 280850064,
    "girdle": "Medium to Slightly Thick",
    "id": "2f189fd8-4393-4d69-a7a1-18a5aff7e8ab",
    "length_mm": 6.72,
    "lot_id": 139258,
    "netsuite_id": 17555,
    "ns_location": "Los Angeles",
    "pavilion_angle": 41.0,
    "pavilion_height": 43.5,
    "polish": "Excellent",
    "prices": [
      {
        "amount_usd": "1816.0",
        "name": "MSRP-40%"
      }
    ],
    "quantity": 1,
    "shape": "Brilliant Round",
    "symmetry": "Excellent",
    "table_size": 57.0,
    "unit_price_msrp_usd": "3027.0",
    "updated_at": "2019-05-20T18:44:28.852Z",
    "width_mm": 6.76
  }
]
```

## /api/v2/diamonds/{id}

`GET https://rest.diamondfoundry.com/api/v2/diamonds/{id}`

Please note valid Authorization header with JWT Token is required.

### Response body 

> Response JSON is structured like this: 

```json
{
  "carat": 3.08,
  "clarity": "VS2",
  "color": "J",
  "created_at": "2019-05-13T18:29:55.960Z",
  "crown_angle": 35.0,
  "crown_height": 15.0,
  "cut_grade": "Excellent",
  "depth_mm": 5.76,
  "depth_pct": 61.8,
  "digital_assets": [],
  "fluorescence": "None",
  "gcal_cert_id": 291020104,
  "girdle": "Medium to Slightly Thick",
  "id": "b2b03602-aea5-4729-af66-570165afa3e0",
  "length_mm": 9.31,
  "lot_id": 209026,
  "netsuite_id": 121007,
  "ns_location": "Los Angeles",
  "pavilion_angle": 40.8,
  "pavilion_height": 43.0,
  "polish": "Very Good",
  "prices": [
    {
      "amount_usd": "12705.0",
      "name": "MSRP-40%"
    }
  ],
  "quantity": 1,
  "shape": "Brilliant Round",
  "symmetry": "Excellent",
  "table_size": 57.0,
  "unit_price_msrp_usd": "14438.0",
  "updated_at": "2019-05-20T18:44:54.679Z",
  "width_mm": 9.34
}
```

# Order V2 Endpoints

Please note valid Authorization header with JWT Token is required.

## /api/v2/orders
`GET https://rest.diamondfoundry.com/api/v2/orders`

Please note valid Authorization header with JWT Token is required.

### Response body 

```json
[
  {
    "created_at": "2019-05-22T20:37:52.567Z",
    "customer_account_id": "ba35e062-f616-424a-aa20-4700051ded68",
    "erp_id": null,
    "id": "dd4d6dfb-45e3-46bf-bfec-108f2eb6d328",
    "order_items": [
      {
        "diamond": {
          "carat": 3.0,
          "clarity": "VVS2",
          "color": "D",
          "cut_grade": "excellent",
          "id": "e273afa9-3d73-48e3-8d24-c27b351bd1f5",
          "lot_id": 60315318040,
          "shape": "oval"
        },
        "id": "ca46aa8d-405b-4bf0-9b2e-53cca70d8272",
        "price_extended": "5694.0",
        "quantity": 1,
        "sold_price": "500.43",
        "tax_collected": null,
        "tax_rate": null
      },
      {
        "diamond": {
          "carat": 3.0,
          "clarity": "VVS2",
          "color": "E",
          "cut_grade": "ideal",
          "id": "63ae1281-ecbb-4876-8475-4342e3300591",
          "lot_id": 209713948362,
          "shape": "round"
        },
        "id": "1ecca3e9-2f2e-4e7f-b4ee-e473c9ef3aa9",
        "price_extended": "14611.0",
        "quantity": 1,
        "sold_price": "500.43",
        "tax_collected": null,
        "tax_rate": null
      },
      {
        "diamond": {
          "carat": 1.0,
          "clarity": "VVS2",
          "color": "F",
          "cut_grade": "ideal",
          "id": "08a79d54-e982-45b2-b20a-3e64ecbfbee8",
          "lot_id": 190552663844,
          "shape": "pear"
        },
        "id": "792a6b8f-9a7a-467f-b134-86616df8fe27",
        "price_extended": "24619.0",
        "quantity": 1,
        "sold_price": "500.43",
        "tax_collected": null,
        "tax_rate": null
      }
    ],
    "shipping_address_id": "84675fd3-bf18-49ef-9cf7-29d6061de57d",
    "source_order_id": 144745417915,
    "updated_at": "2019-05-22T20:37:52.567Z"
  },
  {
    "created_at": "2019-05-23T00:56:14.845Z",
    "customer_account_id": "ba35e062-f616-424a-aa20-4700051ded68",
    "erp_id": null,
    "id": "ccf6b456-8d16-4ad3-bab6-6b70022656fe",
    "order_items": [],
    "shipping_address_id": "48cc0167-d511-43ae-a231-1fc6e26627f8",
    "source_order_id": 151183608411,
    "updated_at": "2019-05-23T00:56:14.845Z"
  },
  {
    "created_at": "2019-05-23T00:56:38.257Z",
    "customer_account_id": "f352f41e-b296-4b62-8095-7088cc4a4038",
    "erp_id": null,
    "id": "d42ecafa-5f49-4763-a5d3-167f828afabe",
    "order_items": [
      {
        "diamond": {
          "carat": 2.0,
          "clarity": "VVS2",
          "color": "D",
          "cut_grade": "ideal",
          "id": "e81be5e6-ef6f-48d1-bad4-e5107e12b6f8",
          "lot_id": 45222641498,
          "shape": "round"
        },
        "id": "151b9049-d28a-457f-840c-02428f81b6ea",
        "price_extended": "15174.0",
        "quantity": 1,
        "sold_price": "500.43",
        "tax_collected": null,
        "tax_rate": null
      }
    ],
    "shipping_address_id": "b890daf5-d71d-4926-9d6e-77d16b3b0a1f",
    "source_order_id": 773525529,
    "updated_at": "2019-05-23T00:56:38.257Z"
  }
]
```

## /api/v2/orders/{id}
`GET https://rest.diamondfoundry.com/api/v2/orders/{id}`

Please note valid Authorization header with JWT Token is required.

### Response body

```json
{
  "created_at": "2019-05-22T20:37:52.567Z",
  "customer_account_id": "ba35e062-f616-424a-aa20-4700051ded68",
  "erp_id": null,
  "id": "dd4d6dfb-45e3-46bf-bfec-108f2eb6d328",
  "order_items": [
    {
      "diamond": {
        "carat": 3.0,
        "clarity": "VVS2",
        "color": "D",
        "cut_grade": "excellent",
        "id": "e273afa9-3d73-48e3-8d24-c27b351bd1f5",
        "lot_id": 60315318040,
        "shape": "oval"
      },
      "id": "ca46aa8d-405b-4bf0-9b2e-53cca70d8272",
      "price_extended": "5694.0",
      "quantity": 1,
      "sold_price": "500.43",
      "tax_collected": null,
      "tax_rate": null
    },
    {
      "diamond": {
        "carat": 3.0,
        "clarity": "VVS2",
        "color": "E",
        "cut_grade": "ideal",
        "id": "63ae1281-ecbb-4876-8475-4342e3300591",
        "lot_id": 209713948362,
        "shape": "round"
      },
      "id": "1ecca3e9-2f2e-4e7f-b4ee-e473c9ef3aa9",
      "price_extended": "14611.0",
      "quantity": 1,
      "sold_price": "500.43",
      "tax_collected": null,
      "tax_rate": null
    },
    {
      "diamond": {
        "carat": 1.0,
        "clarity": "VVS2",
        "color": "F",
        "cut_grade": "ideal",
        "id": "08a79d54-e982-45b2-b20a-3e64ecbfbee8",
        "lot_id": 190552663844,
        "shape": "pear"
      },
      "id": "792a6b8f-9a7a-467f-b134-86616df8fe27",
      "price_extended": "24619.0",
      "quantity": 1,
      "sold_price": "500.43",
      "tax_collected": null,
      "tax_rate": null
    }
  ],
  "shipping_address_id": "84675fd3-bf18-49ef-9cf7-29d6061de57d",
  "source_order_id": 144745417915,
  "updated_at": "2019-05-22T20:37:52.567Z"
}
```

# CustomerAccount Endpoints

**Authentication required

## GET /api/v2/customer_account
`GET https://rest.diamondfoundry.com/api/v2/customer_account`

Valid Authorization header with JWT Token or API key is required.

### Response body
```json
{
  "addresses": [
    {
      "attention": null,
      "city": "Twin Peaks",
      "country": "USA",
      "id": "e1bd3ef1-ce25-401c-90df-d5a2bcbcab1b",
      "line_2": null,
      "line_3": null,
      "name": "Dr. Elizabet Labadie",
      "phone": null,
      "state": "California",
      "street_address": "2505 Oberbrunner Overpass",
      "zip": "92391-3868"
    }
  ],
  "company_name": "Example Co",
  "id": "2b91ac1a-8454-45ef-abea-8aae7beebe95",
  "ns_status": "Purchasing",
  "phone": "(900)999-9999"
}
```