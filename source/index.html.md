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
    "carat": 1.61,
    "clarity": "VS1",
    "color": "I",
    "created_at": "2018-12-20T00:05:53.056Z",
    "crown_angle": 0.0,
    "crown_height": 10.6,
    "cut_grade": "Excellent",
    "depth_mm": 4.53,
    "depth_pct": 71.6,
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
    "updated_at": "2019-01-31T14:43:15.887Z"
  },
  {
    "carat": 2.01,
    "clarity": "VS1",
    "color": "K",
    "created_at": "2019-01-15T22:54:47.121Z",
    "crown_angle": 34.2,
    "crown_height": 12.6,
    "cut_grade": "Excellent",
    "depth_mm": 4.22,
    "depth_pct": 57.9,
    "fluorescence": "None",
    "gcal_cert_id": 281100156,
    "girdle": "Thick to Very Thick",
    "id": "e9f49e1d-dc93-4df5-985c-42de4f946d4d",
    "length_mm": 9.85,
    "lot_id": 148626,
    "netsuite_id": 17969,
    "ns_location": "Los Angeles",
    "pavilion_angle": 39.0,
    "pavilion_height": 40.5,
    "polish": "Excellent",
    "quantity": 1,
    "shape": "Oval",
    "symmetry": "Very Good",
    "table_size": 63.0,
    "unit_price_msrp_usd": "6784.0",
    "updated_at": "2019-01-31T14:22:38.113Z"
  }
]
```

```shell
curl 'https://dfoundry-diamonds.herokuapp.com/api/v1/diamonds'
```

## /api/v1/diamonds query string params
/api/v1/diamonds takes optional query string params in array form for attributes 'shape', 'color', 'cut_grade', and 'clarity'. /api/v1/diamonds also takes 'extended' query string param which optionally nests digital assets within the diamond (for those diamonds that have digital assets associated to it):

### HTTP Request w/ query string params (without extended)
`GET https://dfoundry-diamonds.herokuapp.com/api/v1/diamonds?shape[]=oval&shape[]=pear&color[]=d&color[]=f&color[]=g&color[]=h`

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
    "updated_at": "2019-01-31T14:12:47.427Z"
  },
  {
    "carat": 2.09,
    "clarity": "VS1",
    "color": "H",
    "created_at": "2019-01-11T19:56:18.199Z",
    "crown_angle": 35.2,
    "crown_height": 13.4,
    "cut_grade": "Excellent",
    "depth_mm": 4.28,
    "depth_pct": 58.4,
    "fluorescence": "None",
    "gcal_cert_id": 290020100,
    "girdle": "Thin to Slightly Thick",
    "id": "c48cf772-919f-4eff-a00f-70b2eaa7861a",
    "length_mm": 10.24,
    "lot_id": 200693,
    "netsuite_id": 107689,
    "ns_location": "Los Angeles",
    "pavilion_angle": 38.5,
    "pavilion_height": 41.1,
    "polish": "Very Good",
    "quantity": 1,
    "shape": "Oval",
    "symmetry": "Very Good",
    "table_size": 59.0,
    "unit_price_msrp_usd": "11704.0",
    "updated_at": "2019-01-31T14:22:46.420Z"
  },
  {
    "carat": 2.01,
    "clarity": "VS1",
    "color": "F",
    "created_at": "2019-01-29T02:56:17.211Z",
    "crown_angle": 36.0,
    "crown_height": 14.2,
    "cut_grade": "Excellent",
    "depth_mm": 4.28,
    "depth_pct": 59.6,
    "fluorescence": "None",
    "gcal_cert_id": 290110044,
    "girdle": "Medium to Thick",
    "id": "fd7fcc8b-897a-492d-ab67-a52587e68c81",
    "length_mm": 10.06,
    "lot_id": 202410,
    "netsuite_id": 109427,
    "ns_location": "Los Angeles",
    "pavilion_angle": 38.6,
    "pavilion_height": 41.1,
    "polish": "Excellent",
    "quantity": 1,
    "shape": "Oval",
    "symmetry": "Very Good",
    "table_size": 57.0,
    "unit_price_msrp_usd": "15276.0",
    "updated_at": "2019-01-31T14:22:58.010Z"
  },
  {
    "carat": 1.57,
    "clarity": "VS2",
    "color": "H",
    "created_at": "2019-01-11T19:56:18.998Z",
    "crown_angle": 35.9,
    "crown_height": 13.4,
    "cut_grade": "Excellent",
    "depth_mm": 3.95,
    "depth_pct": 59.3,
    "fluorescence": "None",
    "gcal_cert_id": 290020090,
    "girdle": "Medium to Thick",
    "id": "6e217948-ea45-4671-ac87-92f6b2d11482",
    "length_mm": 9.26,
    "lot_id": 201461,
    "netsuite_id": 107692,
    "ns_location": "Los Angeles",
    "pavilion_angle": 38.7,
    "pavilion_height": 41.4,
    "polish": "Very Good",
    "quantity": 1,
    "shape": "Oval",
    "symmetry": "Very Good",
    "table_size": 59.0,
    "unit_price_msrp_usd": "6272.0",
    "updated_at": "2019-01-31T14:13:15.589Z"
  },
  {
    "carat": 1.39,
    "clarity": "VS2",
    "color": "G",
    "created_at": "2019-01-11T19:56:19.036Z",
    "crown_angle": 35.1,
    "crown_height": 12.5,
    "cut_grade": "Excellent",
    "depth_mm": 3.71,
    "depth_pct": 57.3,
    "fluorescence": "None",
    "gcal_cert_id": 290020163,
    "girdle": "Medium to Slightly Thick",
    "id": "8e7ad523-7732-4e3a-902b-de4e4588cba7",
    "length_mm": 9.0,
    "lot_id": 193156,
    "netsuite_id": 107784,
    "ns_location": "Los Angeles",
    "pavilion_angle": 38.7,
    "pavilion_height": 41.4,
    "polish": "Very Good",
    "quantity": 1,
    "shape": "Oval",
    "symmetry": "Very Good",
    "table_size": 60.0,
    "unit_price_msrp_usd": "5192.0",
    "updated_at": "2019-01-31T14:06:07.619Z"
  }
]
```

## /api/v1/diamonds?extended=t with 'extended' query string param

### HTTP Request w/ query string params (with 'extended')

```json
[
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
    "updated_at": "2019-01-31T14:43:15.887Z"
  },
  {
    "carat": 2.01,
    "clarity": "VS1",
    "color": "K",
    "created_at": "2019-01-15T22:54:47.121Z",
    "crown_angle": 34.2,
    "crown_height": 12.6,
    "cut_grade": "Excellent",
    "depth_mm": 4.22,
    "depth_pct": 57.9,
    "digital_assets": [],
    "fluorescence": "None",
    "gcal_cert_id": 281100156,
    "girdle": "Thick to Very Thick",
    "id": "e9f49e1d-dc93-4df5-985c-42de4f946d4d",
    "length_mm": 9.85,
    "lot_id": 148626,
    "netsuite_id": 17969,
    "ns_location": "Los Angeles",
    "pavilion_angle": 39.0,
    "pavilion_height": 40.5,
    "polish": "Excellent",
    "quantity": 1,
    "shape": "Oval",
    "symmetry": "Very Good",
    "table_size": 63.0,
    "unit_price_msrp_usd": "6784.0",
    "updated_at": "2019-01-31T14:22:38.113Z"
  },
  {
    "carat": 1.12,
    "clarity": "VS1",
    "color": "I",
    "created_at": "2018-12-20T00:04:36.008Z",
    "crown_angle": 34.0,
    "crown_height": 14.5,
    "cut_grade": "Ideal",
    "depth_mm": 4.11,
    "depth_pct": 61.3,
    "digital_assets": [],
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
    "unit_price_msrp_usd": "3427.0",
    "updated_at": "2019-01-31T13:53:02.816Z"
  },
  {
    "carat": 1.7,
    "clarity": "VS2",
    "color": "I",
    "created_at": "2018-12-20T00:05:52.590Z",
    "crown_angle": 34.5,
    "crown_height": 15.0,
    "cut_grade": "Excellent",
    "depth_mm": 4.72,
    "depth_pct": 61.3,
    "digital_assets": [],
    "fluorescence": "None",
    "gcal_cert_id": 281800096,
    "girdle": "Medium",
    "id": "fd88c76d-1f16-446b-a1ad-0da5dd653988",
    "length_mm": 7.68,
    "lot_id": 178667,
    "netsuite_id": 60447,
    "ns_location": "Los Angeles",
    "pavilion_angle": 41.0,
    "pavilion_height": 43.5,
    "polish": "Very Good",
    "quantity": 1,
    "shape": "Brilliant Round",
    "symmetry": "Excellent",
    "table_size": 57.0,
    "unit_price_msrp_usd": "5708.0",
    "updated_at": "2019-01-31T14:14:35.196Z"
  },
  {
    "carat": 1.28,
    "clarity": "VS2",
    "color": "I",
    "created_at": "2019-01-16T19:43:15.113Z",
    "crown_angle": 34.8,
    "crown_height": 12.7,
    "cut_grade": "Very Good",
    "depth_mm": 3.97,
    "depth_pct": 63.1,
    "digital_assets": [],
    "fluorescence": "None",
    "gcal_cert_id": 281240129,
    "girdle": "Slightly Thick to Thick",
    "id": "9fd2ff63-2739-44bb-bb0f-3b1aa2c021d0",
    "length_mm": 6.51,
    "lot_id": 154333,
    "netsuite_id": 29572,
    "ns_location": "Los Angeles",
    "pavilion_angle": 35.2,
    "pavilion_height": 46.6,
    "polish": "Very Good",
    "quantity": 1,
    "shape": "Cushion",
    "symmetry": "Very Good",
    "table_size": 63.0,
    "unit_price_msrp_usd": "3802.0",
    "updated_at": "2019-01-31T14:06:09.775Z"
  },
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
    "updated_at": "2019-01-31T14:06:36.510Z"
  },
  {
    "carat": 1.12,
    "clarity": "SI1",
    "color": "J",
    "created_at": "2018-12-20T00:04:33.822Z",
    "crown_angle": 0.0,
    "crown_height": 13.3,
    "cut_grade": "Very Good",
    "depth_mm": 3.11,
    "depth_pct": 62.4,
    "digital_assets": [],
    "fluorescence": "None",
    "gcal_cert_id": 283060264,
    "girdle": "Slightly Thick",
    "id": "5cc728c5-ba43-447e-b02d-e7de47152db5",
    "length_mm": 7.49,
    "lot_id": 12393,
    "netsuite_id": 14685,
    "ns_location": "Los Angeles",
    "pavilion_angle": 0.0,
    "pavilion_height": 46.2,
    "polish": "Very Good",
    "quantity": 1,
    "shape": "Emerald",
    "symmetry": "Good",
    "table_size": 59.0,
    "unit_price_msrp_usd": "2671.0",
    "updated_at": "2019-01-31T13:53:01.876Z"
  },
  {
    "carat": 1.3,
    "clarity": "VS2",
    "color": "I",
    "created_at": "2019-01-21T23:05:08.891Z",
    "crown_angle": 34.0,
    "crown_height": 14.5,
    "cut_grade": "Ideal",
    "depth_mm": 4.28,
    "depth_pct": 60.4,
    "digital_assets": [
      {
        "kind": "video",
        "url": "https://s3.amazonaws.com/videos.diamondfoundry.com/202714.mp4"
      }
    ],
    "fluorescence": "None",
    "gcal_cert_id": 290040048,
    "girdle": "Thin to Medium",
    "id": "7e0589bf-9623-4723-a9aa-9d6b27e00ed0",
    "length_mm": 7.08,
    "lot_id": 202714,
    "netsuite_id": 108293,
    "ns_location": "Los Angeles",
    "pavilion_angle": 41.0,
    "pavilion_height": 43.0,
    "polish": "Excellent",
    "quantity": 1,
    "shape": "Brilliant Round",
    "symmetry": "Excellent",
    "table_size": 58.0,
    "unit_price_msrp_usd": "3861.0",
    "updated_at": "2019-01-31T14:06:35.861Z"
  }
]
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
  "updated_at": "2019-01-31T14:06:36.510Z"
}
```

```shell
curl 'https://dfoundry-diamonds.herokuapp.com/api/v1/diamonds/122049'
```

This endpoint retrieves a specific diamond.


# Order Endpoints

## Create Order 

### POST /api/v1/orders

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

## GET /api/v1/orders

### HTTP Request

`GET https://dfoundry-diamonds.herokuapp.com/api/v1/orders`

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

`GET https://dfoundry-diamonds.herokuapp.com/api/v1/orders/fb074590-41de-461b-bc10-fbb2a35cb652`

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
    "street_address": "2512 Michian Ave",
    "zip": null
  },
  "source_order_id": 781449461862
}
```