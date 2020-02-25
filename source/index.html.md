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

## Videos

Links to videos are optionally accessible using query string param 'extended' in the /api/v1/diamonds endpoint.

They are nested by default in the /api/v2/diamonds endpoint. 

Not all diamonds have videos.

For videos, the `url` key is a link to the mp3 file. 

All digital assets including videos are served over ```https``` and cdn backed.

For more info see the individual endpoint documentation. 

Using the ```/api/v1/diamonds``` endpoint specifically; to include videos use the 'extended' query string param.

With query string param for digital assets: 

GET ```https://rest.diamondfoundry.com/api/v1/diamonds?extended=t```. 

This is also described a second time in the query param portion of this endpoint documentation.

### HTTP Request

`GET https://rest.diamondfoundry.com/api/v1/diamonds`

```shell
curl 'https://rest.diamondfoundry.com/api/v1/diamonds'
```

> Response body is structured like this:

```json
[
    {
    "carat": 0.3,
    "cert_url": "https://certificate.diamondfoundry.com/download/201664.pdf",
    "clarity": "SI1",
    "color": "J",
    "created_at": "2018-12-20T00:05:07.096Z",
    "crown_angle": 37.4,
    "crown_height": 12.5,
    "cut_grade": "Excellent",
    "depth_mm": 2.02,
    "depth_pct": 60.1,
    "fluorescence": "None",
    "gcal_cert_id": null,
    "girdle": "Medium",
    "graded_by": "GIA Gemologist",
    "id": "6b77c85c-a5b8-4080-a4ac-706e27fb991d",
    "length_mm": 4.88,
    "lot_id": 201664,
    "netsuite_id": 99090,
    "ns_location": "Los Angeles",
    "pavilion_angle": 39.7,
    "pavilion_height": 44.6,
    "polish": "Excellent",
    "quantity": 1,
    "shape": "Emerald",
    "symmetry": "Excellent",
    "table_size": 64.7,
    "unit_price_df_msrp_usd": "229.0",
    "unit_price_msrp_usd": "159.0",
    "updated_at": "2020-02-13T00:42:12.276Z",
    "width_mm": 3.36
  },
  {
    "carat": 0.31,
    "cert_url": "https://certificate.diamondfoundry.com/download/192581.pdf",
    "clarity": "VVS2",
    "color": "K",
    "created_at": "2018-12-20T00:05:49.709Z",
    "crown_angle": 39.1,
    "crown_height": 16.0,
    "cut_grade": "Excellent",
    "depth_mm": 2.08,
    "depth_pct": 61.5,
    "fluorescence": "None",
    "gcal_cert_id": null,
    "girdle": "Thin",
    "graded_by": "GIA Gemologist",
    "id": "17b24a18-9e03-4b80-8e8b-037e56118218",
    "length_mm": 4.87,
    "lot_id": 192581,
    "netsuite_id": 86425,
    "ns_location": "Los Angeles",
    "pavilion_angle": 39.9,
    "pavilion_height": 42.9,
    "polish": "Excellent",
    "quantity": 1,
    "shape": "Emerald",
    "symmetry": "Excellent",
    "table_size": 61.6,
    "unit_price_df_msrp_usd": "241.0",
    "unit_price_msrp_usd": "164.0",
    "updated_at": "2020-02-13T00:42:06.018Z",
    "width_mm": 3.38
  },
  {
    "carat": 0.31,
    "cert_url": "https://certificate.diamondfoundry.com/download/192669.pdf",
    "clarity": "VVS2",
    "color": "K",
    "created_at": "2018-12-20T00:05:49.869Z",
    "crown_angle": 34.9,
    "crown_height": 13.6,
    "cut_grade": "Excellent",
    "depth_mm": 2.07,
    "depth_pct": 61.2,
    "fluorescence": "None",
    "gcal_cert_id": null,
    "girdle": "Medium",
    "graded_by": "GIA Gemologist",
    "id": "5c36f63a-4787-42b1-a4e5-33dfac26aab5",
    "length_mm": 4.86,
    "lot_id": 192669,
    "netsuite_id": 86477,
    "ns_location": "Los Angeles",
    "pavilion_angle": 39.1,
    "pavilion_height": 44.1,
    "polish": "Excellent",
    "quantity": 1,
    "shape": "Emerald",
    "symmetry": "Excellent",
    "table_size": 62.7,
    "unit_price_df_msrp_usd": "241.0",
    "unit_price_msrp_usd": "164.0",
    "updated_at": "2020-02-13T00:42:06.155Z",
    "width_mm": 3.38
  }
]
```

## /api/v1/diamonds query string params
/api/v1/diamonds takes optional query string params in array form for attributes 'shape', 'color', 'cut_grade', and 'clarity'. 

/api/v1/diamonds also takes 'extended' query string param which optionally nests digital assets within the diamond (for those diamonds that have digital assets associated to it):

Please note; to include digital assets (eg links to video files) you must include the `extended` query param. See how to do that below.

See the difference in response bodies below.

### HTTP Request w/ query string params (without extended)
`GET https://rest.diamondfoundry.com/api/v1/diamonds?shape[]=oval&shape[]=pear&color[]=d&color[]=f&color[]=g&color[]=h`

```json
[
  {
    "carat": 0.3,
    "cert_url": "https://certificate.diamondfoundry.com/download/201664.pdf",
    "clarity": "SI1",
    "color": "J",
    "created_at": "2018-12-20T00:05:07.096Z",
    "crown_angle": 37.4,
    "crown_height": 12.5,
    "cut_grade": "Excellent",
    "depth_mm": 2.02,
    "depth_pct": 60.1,
    "fluorescence": "None",
    "gcal_cert_id": null,
    "girdle": "Medium",
    "graded_by": "GIA Gemologist",
    "id": "6b77c85c-a5b8-4080-a4ac-706e27fb991d",
    "length_mm": 4.88,
    "lot_id": 201664,
    "netsuite_id": 99090,
    "ns_location": "Los Angeles",
    "pavilion_angle": 39.7,
    "pavilion_height": 44.6,
    "polish": "Excellent",
    "quantity": 1,
    "shape": "Emerald",
    "symmetry": "Excellent",
    "table_size": 64.7,
    "unit_price_df_msrp_usd": "229.0",
    "unit_price_msrp_usd": "159.0",
    "updated_at": "2020-02-13T00:42:12.276Z",
    "width_mm": 3.36
  },
  {
    "carat": 0.31,
    "cert_url": "https://certificate.diamondfoundry.com/download/192581.pdf",
    "clarity": "VVS2",
    "color": "K",
    "created_at": "2018-12-20T00:05:49.709Z",
    "crown_angle": 39.1,
    "crown_height": 16.0,
    "cut_grade": "Excellent",
    "depth_mm": 2.08,
    "depth_pct": 61.5,
    "fluorescence": "None",
    "gcal_cert_id": null,
    "girdle": "Thin",
    "graded_by": "GIA Gemologist",
    "id": "17b24a18-9e03-4b80-8e8b-037e56118218",
    "length_mm": 4.87,
    "lot_id": 192581,
    "netsuite_id": 86425,
    "ns_location": "Los Angeles",
    "pavilion_angle": 39.9,
    "pavilion_height": 42.9,
    "polish": "Excellent",
    "quantity": 1,
    "shape": "Emerald",
    "symmetry": "Excellent",
    "table_size": 61.6,
    "unit_price_df_msrp_usd": "241.0",
    "unit_price_msrp_usd": "164.0",
    "updated_at": "2020-02-13T00:42:06.018Z",
    "width_mm": 3.38
  },
  {
    "carat": 0.31,
    "cert_url": "https://certificate.diamondfoundry.com/download/192669.pdf",
    "clarity": "VVS2",
    "color": "K",
    "created_at": "2018-12-20T00:05:49.869Z",
    "crown_angle": 34.9,
    "crown_height": 13.6,
    "cut_grade": "Excellent",
    "depth_mm": 2.07,
    "depth_pct": 61.2,
    "fluorescence": "None",
    "gcal_cert_id": null,
    "girdle": "Medium",
    "graded_by": "GIA Gemologist",
    "id": "5c36f63a-4787-42b1-a4e5-33dfac26aab5",
    "length_mm": 4.86,
    "lot_id": 192669,
    "netsuite_id": 86477,
    "ns_location": "Los Angeles",
    "pavilion_angle": 39.1,
    "pavilion_height": 44.1,
    "polish": "Excellent",
    "quantity": 1,
    "shape": "Emerald",
    "symmetry": "Excellent",
    "table_size": 62.7,
    "unit_price_df_msrp_usd": "241.0",
    "unit_price_msrp_usd": "164.0",
    "updated_at": "2020-02-13T00:42:06.155Z",
    "width_mm": 3.38
  }
]
```

## /api/v1/diamonds?extended=t with 'extended' query string param

### More video documentation

* Please note that the url is a link to the digital asset.

- Not all diamonds have a video. 

- Diamonds that have a video or other digital assets have the digital assets nested under the ```digital_assets``` key. See the example response body.

- All videos are served over ```https``` and CDN backed.

### HTTP Request w/ query string params (with 'extended')

```json
[
    {
    "carat": 1.69,
    "cert_url": "https://igionline.com/viewpdf.htm?itemno=LGG1055704",
    "clarity": "VS2",
    "color": "J",
    "created_at": "2019-10-28T17:24:56.284Z",
    "crown_angle": 34.5,
    "crown_height": 15.0,
    "cut_grade": "Ideal",
    "depth_mm": 4.72,
    "depth_pct": 61.6,
    "digital_assets": [
      {
        "kind": "video",
        "url": "https://videos.diamondfoundry.com/223615.mp4"
      }
    ],
    "fluorescence": "None",
    "gcal_cert_id": null,
    "girdle": "Medium",
    "graded_by": "IGI",
    "id": "c1803174-9418-437e-8d35-326c9a1dcfab",
    "length_mm": 7.7,
    "lot_id": 223615,
    "netsuite_id": 232508,
    "ns_location": "Los Angeles",
    "pavilion_angle": 40.8,
    "pavilion_height": 43.0,
    "polish": "Excellent",
    "quantity": 1,
    "shape": "Brilliant Round",
    "symmetry": "Excellent",
    "table_size": 57.0,
    "unit_price_df_msrp_usd": "4740.0",
    "unit_price_msrp_usd": "3346.0",
    "updated_at": "2020-02-13T00:42:09.332Z",
    "width_mm": 7.64
  },
    {
    "carat": 1.16,
    "cert_url": "https://images.gemfacts.com/GCALimages/Certs/182001.pdf",
    "clarity": "VS1",
    "color": "I",
    "created_at": "2018-12-20T00:05:40.907Z",
    "crown_angle": 34.5,
    "crown_height": 15.0,
    "cut_grade": "Ideal",
    "depth_mm": 4.15,
    "depth_pct": 61.1,
    "digital_assets": [],
    "fluorescence": "None",
    "gcal_cert_id": "281870040",
    "girdle": "Medium",
    "graded_by": "GCAL",
    "id": "95712031-e565-4dc0-9347-9e05deb37464",
    "length_mm": 6.77,
    "lot_id": 182001,
    "netsuite_id": 63437,
    "ns_location": "Los Angeles",
    "pavilion_angle": 41.0,
    "pavilion_height": 43.0,
    "polish": "Excellent",
    "quantity": 1,
    "shape": "Brilliant Round",
    "symmetry": "Excellent",
    "table_size": 57.0,
    "unit_price_df_msrp_usd": "3550.0",
    "unit_price_msrp_usd": "2366.0",
    "updated_at": "2020-02-13T00:42:13.570Z",
    "width_mm": 6.8
  },
  {
    "carat": 1.16,
    "cert_url": "https://igionline.com/viewpdf.htm?itemno=LGG1072916",
    "clarity": "VS2",
    "color": "I",
    "created_at": "2019-12-31T19:01:19.957Z",
    "crown_angle": 35.1,
    "crown_height": 13.3,
    "cut_grade": "Very Good",
    "depth_mm": 3.24,
    "depth_pct": 60.8,
    "digital_assets": [
      {
        "kind": "video",
        "url": "https://videos.diamondfoundry.com/236280.mp4"
      }
    ],
    "fluorescence": "None",
    "gcal_cert_id": null,
    "girdle": "Slightly Thick to Thick",
    "graded_by": "IGI",
    "id": "2cce39d3-b739-4cad-ab64-5b3473cc381f",
    "length_mm": 7.6,
    "lot_id": 236280,
    "netsuite_id": 254645,
    "ns_location": "Los Angeles",
    "pavilion_angle": 39.4,
    "pavilion_height": 43.2,
    "polish": "Excellent",
    "quantity": 1,
    "shape": "Emerald",
    "symmetry": "Excellent",
    "table_size": 63.0,
    "unit_price_df_msrp_usd": "3445.0",
    "unit_price_msrp_usd": "2181.0",
    "updated_at": "2020-02-13T20:23:58.642Z",
    "width_mm": 5.33
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
    "carat": 1.01,
    "cert_url": "https://igionline.com/viewpdf.htm?itemno=LGG1062812",
    "clarity": "VS2",
    "color": "I",
    "created_at": "2019-10-31T00:08:48.649Z",
    "crown_angle": 36.8,
    "crown_height": 10.5,
    "cut_grade": "Excellent",
    "depth_mm": 3.82,
    "depth_pct": 68.0,
    "digital_assets": [
      {
        "kind": "video",
        "url": "https://videos.diamondfoundry.com/231683.mp4"
      }
    ],
    "fluorescence": "None",
    "gcal_cert_id": null,
    "girdle": "Medium",
    "graded_by": "IGI",
    "id": "8e33d97a-08aa-484f-9878-516e638f5f36",
    "length_mm": 5.62,
    "lot_id": 231683,
    "netsuite_id": 238842,
    "ns_location": "Los Angeles",
    "pavilion_angle": 37.3,
    "pavilion_height": 54.3,
    "polish": "Excellent",
    "prices": [
      {
        "amount_usd": "1329.0",
        "name": "Partner"
      }
    ],
    "quantity": 1,
    "shape": "Princess",
    "symmetry": "Very Good",
    "table_size": 68.0,
    "unit_price_msrp_usd": "1899.0",
    "updated_at": "2020-02-13T20:24:14.723Z",
    "width_mm": 5.78
  },
  {
    "carat": 1.18,
    "cert_url": "https://certificate.diamondfoundry.com/download/228906.pdf",
    "clarity": "VS1",
    "color": "J",
    "created_at": "2019-12-17T18:23:37.991Z",
    "crown_angle": 35.0,
    "crown_height": 15.0,
    "cut_grade": "Excellent",
    "depth_mm": 4.2,
    "depth_pct": 62.0,
    "digital_assets": [
      {
        "kind": "video",
        "url": "https://videos.diamondfoundry.com/228906.mp4"
      }
    ],
    "fluorescence": "None",
    "gcal_cert_id": null,
    "girdle": "Thin to Medium",
    "graded_by": "IGI",
    "id": "038e73ea-aa1f-488a-920a-320d902595e9",
    "length_mm": 6.77,
    "lot_id": 228906,
    "netsuite_id": 249210,
    "ns_location": "Los Angeles",
    "pavilion_angle": 40.9,
    "pavilion_height": 43.0,
    "polish": "Excellent",
    "prices": [
      {
        "amount_usd": "1462.0",
        "name": "Partner"
      }
    ],
    "quantity": 1,
    "shape": "Brilliant Round",
    "symmetry": "Excellent",
    "table_size": 56.5,
    "unit_price_msrp_usd": "2089.0",
    "updated_at": "2020-02-13T00:42:05.816Z",
    "width_mm": 6.8
  },
  {
    "carat": 1.19,
    "cert_url": "https://certificate.diamondfoundry.com/download/228972.pdf",
    "clarity": "VS1",
    "color": "J",
    "created_at": "2019-12-17T18:25:10.823Z",
    "crown_angle": 34.5,
    "crown_height": 14.5,
    "cut_grade": "Excellent",
    "depth_mm": 4.18,
    "depth_pct": 61.3,
    "digital_assets": [
      {
        "kind": "video",
        "url": "https://videos.diamondfoundry.com/228972.mp4"
      }
    ],
    "fluorescence": "Very Slight",
    "gcal_cert_id": null,
    "girdle": "Thin to Medium",
    "graded_by": "IGI",
    "id": "f8ae233d-87c0-40db-b139-1ca7c6aaee3b",
    "length_mm": 6.79,
    "lot_id": 228972,
    "netsuite_id": 250424,
    "ns_location": "Los Angeles",
    "pavilion_angle": 40.8,
    "pavilion_height": 43.0,
    "polish": "Excellent",
    "prices": [
      {
        "amount_usd": "1474.0",
        "name": "Partner"
      }
    ],
    "quantity": 1,
    "shape": "Brilliant Round",
    "symmetry": "Excellent",
    "table_size": 57.5,
    "unit_price_msrp_usd": "2106.0",
    "updated_at": "2020-02-13T00:42:05.335Z",
    "width_mm": 6.86
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
  "carat": 1.01,
  "cert_url": "https://igionline.com/viewpdf.htm?itemno=LGG1062812",
  "clarity": "VS2",
  "color": "I",
  "created_at": "2019-10-31T00:08:48.649Z",
  "crown_angle": 36.8,
  "crown_height": 10.5,
  "cut_grade": "Excellent",
  "depth_mm": 3.82,
  "depth_pct": 68.0,
  "digital_assets": [
    {
      "kind": "video",
      "url": "https://videos.diamondfoundry.com/231683.mp4"
    }
  ],
  "fluorescence": "None",
  "gcal_cert_id": null,
  "girdle": "Medium",
  "graded_by": "IGI",
  "id": "8e33d97a-08aa-484f-9878-516e638f5f36",
  "length_mm": 5.62,
  "lot_id": 231683,
  "netsuite_id": 238842,
  "ns_location": "Los Angeles",
  "pavilion_angle": 37.3,
  "pavilion_height": 54.3,
  "polish": "Excellent",
  "prices": [
    {
      "amount_usd": "1329.0",
      "name": "Partner"
    }
  ],
  "quantity": 1,
  "shape": "Princess",
  "symmetry": "Very Good",
  "table_size": 68.0,
  "unit_price_msrp_usd": "1899.0",
  "updated_at": "2020-02-13T20:24:14.723Z",
  "width_mm": 5.78
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

