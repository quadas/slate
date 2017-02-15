---
title: Quadas API Reference

language_tabs:
  - shell

toc_footers:

includes:
  - errors

search: false
---

# Introduction

Welcome to the Publisher API! You can use our API to access Publisher API endpoints, which can CRUD your owned publishers. The API is organized around REST. Our API has predictable, resource-oriented URLs, and uses HTTP response codes to indicate API errors. We use built-in HTTP features, like HTTP authentication and HTTP verbs, which are understood by off-the-shelf HTTP clients.

# Access Token

Please retrieve your own token before accessing other resources.

> Example Request:

```
curl --data "username=USERNAME&password=PASSWORD" \
  --referer http://UI_HOST \
  -X POST http://HOST/api/users/sessions
```

> Example Response:

```json
{ "token": "NO_USE|ACCESS_TOKEN" }
```

### HTTP Request

`POST http://HOST/api/users/sessions`

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
username | true | The username of your account
password | true | The password of your account

<aside class="warning">
The response consists of two parts, checksum and access token, which are separated by a <code>|</code>.

You could drop the checksum part directly, for only access token is required in the future requests.
</aside>

# Authentication

> Example Request:

```shell
curl -H X-Requested-With: XMLHttpRequest \
  -H x-access-token: TOKEN \
  "http://HOST/api/publishers"
```

To authorize, just inject the pairs below into your request header:

- `X-Requested-With: XMLHttpRequest`
- `x-access-token: TOKEN`

<aside class="notice">
You must replace <code>TOKEN</code> with your access token.
</aside>

# Publishers

## Get All Publishers

> Example Request:

```shell
curl -H "X-Requested-With: XMLHttpRequest" \
     -H "x-access-token: TOKEN" \
     http://HOST/api/publishers
```

> Example Response:

```json
{
  "data": [
    {
      "publisher_state":0,
      "impressions":0,
      "publisher_revenue":0.0,
      "ssp_platform_ecpm":null,
      "placements_count":0,
      "exchange_rate_markup":0.0,
      "blank_impressions":0,
      "publisher_ecpm":null,
      "kept_impressions":0,
      "resold_impressions":0,
      "ssp_platform_profit":0.0,
      "fill_rate":null,
      "publisher_id":"20",
      "trade_logs":0,
      "amount":0.0,
      "ssp_platform_revenue":0.0,
      "default_impressions":0,
      "interval":"2017-01-25T00:00:00.000+08:00/2017-01-25T11:00:00.000+08:00",
      "start_at":1485273600000,
      "clicks":0,
      "created_at":1485310223117,
      "ctr":null,
      "publisher_name":"test publisher",
      "seller_revenue_share":0.0,
      "requests":0,
      "ssp_platform_ecpc":null,
      "end_at":1485313200000,
      "publisher_ecpc":null
    }
  ],
  "summary": {
    "impressions":0,
    "publisher_revenue": 0.0,
    "ssp_platform_ecpm": null,
    "exchange_rate_markup":0.0,
    "blank_impressions":0,
    "publisher_ecpm":null,
    "kept_impressions":0,
    "resold_impressions":0,
    "ssp_platform_profit":0.0,
    "fill_rate":null,
    "trade_logs":0,
    "amount":0.0,
    "ssp_platform_revenue":0.0,
    "default_impressions":0,
    "clicks":0,
    "ctr":null,
    "seller_revenue_share":0.0,
    "requests":0,
    "ssp_platform_ecpc":null,
    "publisher_ecpc":null
  },
  "meta": { "total": 1 }
}
```

### HTTP Request

`GET http://HOST/api/publishers`

### Query Parameters

Parameter    | Required | Default | Type |  Description
------------ | -------- | ------- | ---- |  -----------
platform_id | true | 0 | string | ID of platform, also known as 'SSP Id'
publisher_ids | false | None | string | ID of publishers
state | false | 0 | string | states, eg: 0,1,2
keyword | false | None | string | keyword for publisher name
interval | false | summation | string | Interval
start_at | false | 0 | string | Start At, unix timestamp at milliseconds
end_at | false | None | string | End At, unix timestamp at milliseconds
order | false | publisher_ids,desc;start_at,desc | string | Order. eg: requests,desc;ctr,asc. supported ordering fields: "start_at", "requests", "clicks", "impressions", "effective_impressions", "blank_impressions", "default_impressions", "psa_impressions", "kept_impressions", "resold_impressions", "rtb_impressions", "external_impression_impressions", "external_click_impressions", "cpm_bids", "cpc_bids", "cpa_bids", "amount", "exchange_rate_markup", "seller_revenue_share", "publisher_revenue", "ssp_platform_revenue", "ssp_platform_profit", "fill_rate", "ctr", "publisher_ecpm", "publisher_ecpc", "ssp_platform_ecpm", "ssp_platform_ecpc", "publisher_id", "publisher_name", "publisher_state", "placements_count", "publisher_created_at"
offset | false | 0 | long | Offset
limit | false | 25 | long | Limit
currency | false | JPY | string | Currency. Support: USD,CNY,JPY,TWD,HKD
timezone | false | Asia/Shanghai | string | Timezone, eg: Asia/Shanghai


## Get a Specific Publisher

> Example Request:

```shell
curl -H "X-Requested-With: XMLHttpRequest" \
     -H "x-access-token: TOKEN" \
     http://HOST/api/publisher/1
```

> Example Response:

```json
{
  "actives_count": 4,
  "country_id": "China",
  "cpc_deal": false,
  "cpm_deal": true,
  "currency": "TWD",
  "email": "cloud.li@vpon.com",
  "id": 7,
  "name": "test publisher",
  "payment_term": {
    "apply_served": false,
    "cpm_price": 3,
    "id": 7,
    "pricing_type": "cpm",
    "publisher_id": 7,
    "revenue_share_rate": null,
    "revenue_share_rate_percentage": null
  },
  "placements_count": 4,
  "state": "active",
  "username": "testtest"
}
```

### HTTP Request

`GET http://HOST/api/publisher/:id`

### Query Parameters

Parameter | Required | Default | Description
--------- | -------- | ------- | -----------
id | true | None |

## Create a Publisher

> Example Request:

```
curl -H "X-Requested-With: XMLHttpRequest" \
     -H "x-access-token: TOKEN" \
     --data "publisher[name]=a&publisher[email]=a@a.com&publisher[state]=0&publisher[cpm_deal]=1&publisher[payment_term_attributes][id]=1&&publisher[payment_term_attributes][pricing_type]=4&cpm_price=2"
     -X POST \
     http://HOST/api/publishers
```

> Example Response:

```json
{}
```

### HTTP Request

`POST http://HOST/api/publishers`

### Query Parameters

Parameter | Required| Type | Description
--------- | ------- | ---- | -----------
publisher | true    | PublisherDAO

#### PublihserDAO
Key | Required | Type | Description
--- | ----- | --- | ---
name | true | string |
state | true | ENUM | 0 - ACTIVE, 1 - INACTIVE, 2 - DELETED
currency | true | string |
country_id | true | string | Afghanistan,Albania,Algeria,American Samoa,Andorra,Angola,Anguilla,Antarctica,Antigua and Barbuda,Argentina,Armenia,Aruba,Australia,Austria,Azerbaijan,Bahamas,Bahrain,Bangladesh,Barbados,Belarus,Belgium,Belize,Benin,Bermuda,Bhutan,Bolivia,Bonaire,Bosnia and Herzegovina,Botswana,Bouvet Island,Brazil,British Indian Ocean Territory,Brunei Darussalam,Bulgaria,Burkina Faso,Burundi,Cambodia,Cameroon,Canada,Cape Verde,Cayman Islands,Central African Republic,Chad,Chile,China,Christmas Island,Cocos (Keeling) Islands,Colombia,Comoros,Congo,Democratic Republic of the Congo,Cook Islands,Costa Rica,Croatia,Cuba,CuraÃ§ao,Cyprus,Czech Republic,CÃ´te d'Ivoire,Denmark,Djibouti,Dominica,Dominican Republic,Ecuador,Egypt,El Salvador,Equatorial Guinea,Eritrea,Estonia,Ethiopia,Falkland Islands (Malvinas),Faroe Islands,Fiji,Finland,France,French Guiana,French Polynesia,French Southern Territories,Gabon,Gambia,Georgia,Germany,Ghana,Gibraltar,Greece,Greenland,Grenada,Guadeloupe,Guam,Guatemala,Guernsey,Guinea,Guinea-Bissau,Guyana,Haiti,Heard Island and McDonald Mcdonald Islands,Holy See (Vatican City State),Honduras,Hong Kong,Hungary,Iceland,India,Indonesia,Iran, Islamic Republic of,Iraq,Ireland,Isle of Man,Israel,Italy,Jamaica,Japan,Jersey,Jordan,Kazakhstan,Kenya,Kiribati,Korea, Democratic People's Republic of,Korea, Republic of,Kuwait,Kyrgyzstan,Lao People's Democratic Republic,Latvia,Lebanon,Lesotho,Liberia,Libya,Liechtenstein,Lithuania,Luxembourg,Macao,Macedonia, the Former Yugoslav Republic of,Madagascar,Malawi,Malaysia,Maldives,Mali,Malta,Marshall Islands,Martinique,Mauritania,Mauritius,Mayotte,Mexico,Micronesia, Federated States of,Moldova, Republic of,Monaco,Mongolia,Montenegro,Montserrat,Morocco,Mozambique,Myanmar,Namibia,Nauru,Nepal,Netherlands,New Caledonia,New Zealand,Nicaragua,Niger,Nigeria,Niue,Norfolk Island,Northern Mariana Islands,Norway,Oman,Pakistan,Palau,Palestine, State of,Panama,Papua New Guinea,Paraguay,Peru,Philippines,Pitcairn,Poland,Portugal,Puerto Rico,Qatar,Romania,Russian Federation,Rwanda,Reunion,Saint Barthalemy,Saint Helena,Saint Kitts and Nevis,Saint Lucia,Saint Martin (French part),Saint Pierre and Miquelon,Saint Vincent and the Grenadines,Samoa,San Marino,Sao Tome and Principe,Saudi Arabia,Senegal,Serbia,Seychelles,Sierra Leone,Singapore,Sint Maarten (Dutch part),Slovakia,Slovenia,Solomon Islands,Somalia,South Africa,South Georgia and the South Sandwich Islands,South Sudan,Spain,Sri Lanka,Sudan,Suriname,Svalbard and Jan Mayen,Swaziland,Sweden,Switzerland,Syrian Arab Republic,Taiwan,Tajikistan,United Republic of Tanzania,Thailand,Timor-Leste,Togo,Tokelau,Tonga,Trinidad and Tobago,Tunisia,Turkey,Turkmenistan,Turks and Caicos Islands,Tuvalu,Uganda,Ukraine,United Arab Emirates,United Kingdom,United States,United States Minor Outlying Islands,Uruguay,Uzbekistan,Vanuatu,Venezuela,Viet Nam,British Virgin Islands,US Virgin Islands,Wallis and Futuna,Western Sahara,Yemen,Zambia,Zimbabwe,Aland Islands
payment_term_attributes | true | PaymentTermDAO
email | false | string | valid email address
cpm_deal | false | bool | deal type
force_save | false | bool | set it to true if you want to violate the reserved price

#### PaymentTermDAO
Key | Required | Type | Description
--- | -------- | ---- | ----------
pricing_type | true | ENUM | 4 - CPM, 5 - REVENUE SHARE RATE
cpm_price | false | float | it is required only if pricing type is CPM
revenue_share_rate | false | float | it is required only if pricing type is REVENUE SHARE RATE and revenue_share_rate_percentage is absent
revenue_share_rate_percentage | false | float | 0 ~ 1

## Update a Specific Publisher or Batch Update Publishers

> Example Request:

```
curl -H "X-Requested-With: XMLHttpRequest" \
     -H "x-access-token: TOKEN" \
     --data "publisher[name]=a&publisher[email]=a@a.com&publisher[state]=0&publisher[cpm_deal]=1&publisher[payment_term_attributes][id]=1&&publisher[payment_term_attributes][pricing_type]=4&cpm_price=2"
     -X PUT \
     http://HOST/api/publishers
```

> Example Response:

```json
{}
```

### HTTP Request

`PUT http://HOST/api/publisher/:ids`

### Query Parameters

Parameter | Required| Type | Description
--------- | ------- | ---- | -----------
ids       | true    | string | 1,2,3,4
publisher | true    | PublisherDAO |

#### PublihserDAO
Key | Required | Type | Description
--- | ----- | --- | ---
name | false | string |
state | false | ENUM | 0 - ACTIVE, 1 - INACTIVE, 2 - DELETED
currency | false | string | USD,CNY,JPY,TWD,HKD
country_id | false | string | Afghanistan,Albania,Algeria,American Samoa,Andorra,Angola,Anguilla,Antarctica,Antigua and Barbuda,Argentina,Armenia,Aruba,Australia,Austria,Azerbaijan,Bahamas,Bahrain,Bangladesh,Barbados,Belarus,Belgium,Belize,Benin,Bermuda,Bhutan,Bolivia,Bonaire,Bosnia and Herzegovina,Botswana,Bouvet Island,Brazil,British Indian Ocean Territory,Brunei Darussalam,Bulgaria,Burkina Faso,Burundi,Cambodia,Cameroon,Canada,Cape Verde,Cayman Islands,Central African Republic,Chad,Chile,China,Christmas Island,Cocos (Keeling) Islands,Colombia,Comoros,Congo,Democratic Republic of the Congo,Cook Islands,Costa Rica,Croatia,Cuba,CuraÃ§ao,Cyprus,Czech Republic,CÃ´te d'Ivoire,Denmark,Djibouti,Dominica,Dominican Republic,Ecuador,Egypt,El Salvador,Equatorial Guinea,Eritrea,Estonia,Ethiopia,Falkland Islands (Malvinas),Faroe Islands,Fiji,Finland,France,French Guiana,French Polynesia,French Southern Territories,Gabon,Gambia,Georgia,Germany,Ghana,Gibraltar,Greece,Greenland,Grenada,Guadeloupe,Guam,Guatemala,Guernsey,Guinea,Guinea-Bissau,Guyana,Haiti,Heard Island and McDonald Mcdonald Islands,Holy See (Vatican City State),Honduras,Hong Kong,Hungary,Iceland,India,Indonesia,Iran, Islamic Republic of,Iraq,Ireland,Isle of Man,Israel,Italy,Jamaica,Japan,Jersey,Jordan,Kazakhstan,Kenya,Kiribati,Korea, Democratic People's Republic of,Korea, Republic of,Kuwait,Kyrgyzstan,Lao People's Democratic Republic,Latvia,Lebanon,Lesotho,Liberia,Libya,Liechtenstein,Lithuania,Luxembourg,Macao,Macedonia, the Former Yugoslav Republic of,Madagascar,Malawi,Malaysia,Maldives,Mali,Malta,Marshall Islands,Martinique,Mauritania,Mauritius,Mayotte,Mexico,Micronesia, Federated States of,Moldova, Republic of,Monaco,Mongolia,Montenegro,Montserrat,Morocco,Mozambique,Myanmar,Namibia,Nauru,Nepal,Netherlands,New Caledonia,New Zealand,Nicaragua,Niger,Nigeria,Niue,Norfolk Island,Northern Mariana Islands,Norway,Oman,Pakistan,Palau,Palestine, State of,Panama,Papua New Guinea,Paraguay,Peru,Philippines,Pitcairn,Poland,Portugal,Puerto Rico,Qatar,Romania,Russian Federation,Rwanda,Reunion,Saint Barthalemy,Saint Helena,Saint Kitts and Nevis,Saint Lucia,Saint Martin (French part),Saint Pierre and Miquelon,Saint Vincent and the Grenadines,Samoa,San Marino,Sao Tome and Principe,Saudi Arabia,Senegal,Serbia,Seychelles,Sierra Leone,Singapore,Sint Maarten (Dutch part),Slovakia,Slovenia,Solomon Islands,Somalia,South Africa,South Georgia and the South Sandwich Islands,South Sudan,Spain,Sri Lanka,Sudan,Suriname,Svalbard and Jan Mayen,Swaziland,Sweden,Switzerland,Syrian Arab Republic,Taiwan,Tajikistan,United Republic of Tanzania,Thailand,Timor-Leste,Togo,Tokelau,Tonga,Trinidad and Tobago,Tunisia,Turkey,Turkmenistan,Turks and Caicos Islands,Tuvalu,Uganda,Ukraine,United Arab Emirates,United Kingdom,United States,United States Minor Outlying Islands,Uruguay,Uzbekistan,Vanuatu,Venezuela,Viet Nam,British Virgin Islands,US Virgin Islands,Wallis and Futuna,Western Sahara,Yemen,Zambia,Zimbabwe,Aland Islands
payment_term_attributes | true | PaymentTermDAO
email | false | string | valid email address
cpm_deal | false | bool | deal type
force_save | false | bool | set it to true if you want to violate the reserved price

#### PaymentTermDAO
Key | Required | Type | Description
--- | -------- | ---- | ----------
pricing_type | true | ENUM | 4 - CPM, 5 - REVENUE SHARE RATE
cpm_price | false | float | it is required only if pricing type is CPM
revenue_share_rate | false | float | it is required only if pricing type is REVENUE SHARE RATE and revenue_share_rate_percentage is absent
revenue_share_rate_percentage | false | float | 0 ~ 1

# Placements

## Get All Placements

> Example Request:

```shell
curl -H "X-Requested-With: XMLHttpRequest" \
     -H "x-access-token: TOKEN" \
     http://HOST/api/publishers/:publisher_id/placements
```

> Example Response:

```json
{
  "data": [
    {
      "publisher_state":0,
      "impressions":0,
      "publisher_revenue":0.0,
      "ssp_platform_ecpm":null,
      "placements_count":4,
      "exchange_rate_markup":0.0,
      "blank_impressions":0,
      "publisher_ecpm":null,
      "kept_impressions":0,
      "resold_impressions":0,
      "ssp_platform_profit":0.0,
      "fill_rate":null,
      "publisher_id":"7",
      "placement_group_id":"13",
      "trade_logs":0,
      "amount":0.0,
      "ssp_platform_revenue":0.0,
      "default_impressions":0,
      "interval":"2017-01-24T16:00:00.000Z/2017-01-25T03:00:00.000Z",
      "start_at":1485273600000,
      "clicks":0,
      "created_at":1477029059253,
      "ctr":null,
      "placement_state":0,
      "publisher_name":"test 2",
      "seller_revenue_share":0.0,
      "requests":0,
      "ssp_platform_ecpc":null,
      "end_at":1485313200000,
      "publisher_ecpc":null,
      "placement_id":"63",
      "placement_name":"test_placement"
    }
  ],
  "summary": {
    "impressions":0,
    "publisher_revenue":0.0,
    "ssp_platform_ecpm":null,
    "exchange_rate_markup":0.0,
    "blank_impressions":0,
    "publisher_ecpm":null,
    "kept_impressions":0,
    "resold_impressions":0,
    "ssp_platform_profit":0.0,
    "fill_rate":null,
    "trade_logs":0,
    "amount":0.0,
    "ssp_platform_revenue":0.0,
    "default_impressions":0,
    "clicks":0,
    "ctr":null,
    "seller_revenue_share":0.0,
    "requests":0,
    "ssp_platform_ecpc":null,
    "publisher_ecpc":null
  },
  "meta": { "total": 1 }
}
```

### HTTP Request

`GET http://HOST/api/publishers/:publisher_id/placements`

### Query Parameters

Key | Required | Default | Type | Description
----| -------- | ------- | ---  | -------------
publisher_id | true | None | string | ID of Publisher
platform_id | true | 0 | string | ID of platform, also known as 'SSP Id'
placement_ids | false | None | string | ID of Placements
placement_group_ids | false | None | string | ID of Placement Groups
state | false | 0 | string | states, eg: 0,1,2
keyword | false | None | string | keyword for Placement name
start_at | false | 0 | string | Start At, unix timestamp at milliseconds
end_at | false | None | string | End At, unix timestamp at milliseconds
order | false | placement_ids,desc;start_at,desc | string | Order. eg: requests,desc;ctr,asc. supported ordering fields: "start_at", "requests", "clicks", "impressions", "effective_impressions", "blank_impressions", "default_impressions", "psa_impressions", "kept_impressions", "resold_impressions", "rtb_impressions", "external_impression_impressions", "external_click_impressions", "cpm_bids", "cpc_bids", "cpa_bids", "amount", "exchange_rate_markup", "seller_revenue_share", "Placement_revenue", "ssp_platform_revenue", "ssp_platform_profit", "fill_rate", "ctr", "Placement_ecpm", "Placement_ecpc", "ssp_platform_ecpm", "ssp_platform_ecpc", "placement_id", "placement_group_id", "placement_name", "placement_state", "placements_count", "placement_created_at"
interval | false | summation | string | Interval
include_empty_row | false | 0 | long | 0 for false, 1 for true
offset | false | 0 | long | Offset
limit | false | 25 | long | Limit
currency | false | JPY | string | Currency. Support: USD,CNY,JPY,TWD,HKD
timezone | false | Asia/Shanghai | string | Timezone, eg: Asia/Shanghai

## Get a Specific Placement

> Example Request:

```shell
curl -H "X-Requested-With: XMLHttpRequest" \
     -H "x-access-token: TOKEN" \
     http://HOST/api/publishers/PUBLISHER_ID/placement_groups/PLACMENT_GROUP_ID/placements/PLACEMENT_ID
```

> Example Response:

```json
{
  "id": 1,
  "name": "name",
  "state": "archive",
  "size": "300x200",
  "media_type": "banner",
  "universal_categories": {},
  "categories_data": [],
  "placement_grouop_id": 1,
  "group_categories_data": [],
  "has_creative": false,
  "creative": null,
  "has_reserve_price": false,
  "cpm_deal": 1,
  "cpc_deal": 1,
  "currency": "USD"
}
```

### HTTP Request
`GET http://HOST/api/publishers/:publisher_id/placement_groups/:placement_group_id/placements/:id`

### Query Parameters

Parameter | Required | Default | Description
--------- | -------- | ------- | -----------
id        | true | None |
publisher_id | true | None |
placement_group_id | true | None |

## Duplicate Placements

> Example Request:

```shell
curl -H "X-Requested-With: XMLHttpRequest" \
     -H "x-access-token: TOKEN" \
     --data "placements[][placement_id]=1&placements[][name]=name"
     -X POST \
     http://HOST/api/publishers/PUBLISHER_ID/placements
```

> Example Response:

```json
// 201
```

### HTTP Request
`POST http://HOST/api/publishers/:publisher_id/placements/duplicate`

### Query Parameters

Parameter | Required | Default | Description
--------- | -------- | ------- | -----------
placements | true | None |

#### PlacementDuplicateDAO

Key | Required | Default | Description
--------- | -------- | ------- | -----------
placemng_id | true | None |
name | true | None |

## Update a Specific Placements or Batch Update Placements

> Example Request:

```shell
curl -H "X-Requested-With: XMLHttpRequest" \
     -H "x-access-token: TOKEN" \
     -X PUT \
     --data "name=another_name"
     http://HOST/api/publishers/:publisher_id/placement_groups/:placement_group_id/placements/:ids
```

> Example Response:

```json
// 204
```

### HTTP Request
`PUT http://HOST/api/publishers/:publisher_id/placement_groups/:placement_group_id/placements/:ids`

### Query Parameters

Parameter | Required | Default | Description
--------- | -------- | ------- | -----------
ids | true | None | 1,2,3,4
publisher_id | true | None |
placement_group_id | true | None |
placement | true | None | PlacementDAO

#### PlacementDAO

Key | Required | Type | Description
--------- | -------- | ------- | -----------
name | false | string |
state | false | ENUM | 0 - ACTIVE, 1 - INACTIVE, 2 - DELETED
has_reserve_price | false | integer | 1 or 0
cpm_price | false | float |
width | false |integer |
height | false | integer |
size | false | string | 200x100 . it is required for placements whose media type is banner
position | false | string | requisite for video. Available values: any / pre_roll / mid_roll / post_roll
max_duration | false | int | requisite for video
skippable | false | bool | requisite for video
media_type | false | string | banner / interstitial / native / video

## Export Tag of a Specific Placement

> Example Request:

```shell
curl -H "X-Requested-With: XMLHttpRequest" \
     -H "x-access-token: TOKEN" \
     http://HOST/api/publishers/:publisher_id/placements/:id/export_tag
```

> Example Response:

```json
{
  "placement_id": "1_2",
  "tag": "<div id=\"1_2\"></div><script>code here</script>"
}
```

### HTTP Request
`GET http://HOST/api/publishers/:publisher_id/placements/:id/export_tag`

### Query Parameters

Parameter | Required | Default | Description
--------- | -------- | ------- | -----------
publisher_id | true | None |
id | true | None |

## Get All Placements Under a Specific Placement Group

> Example Request:

```shell
curl -H "X-Requested-With: XMLHttpRequest" \
     -H "x-access-token: TOKEN" \
     http://HOST/api/publishers/:publisher_id/placement_groups/:placement_group_id/placements
```

> Example Response:

```json
{
  "data": [
    {
      "publisher_state":0,
      "impressions":0,
      "publisher_revenue":0.0,
      "ssp_platform_ecpm":null,
      "placements_count":4,
      "exchange_rate_markup":0.0,
      "blank_impressions":0,
      "publisher_ecpm":null,
      "kept_impressions":0,
      "resold_impressions":0,
      "ssp_platform_profit":0.0,
      "fill_rate":null,
      "publisher_id":"7",
      "placement_group_id":"13",
      "trade_logs":0,
      "amount":0.0,
      "ssp_platform_revenue":0.0,
      "default_impressions":0,
      "interval":"2017-01-24T16:00:00.000Z/2017-01-25T03:00:00.000Z",
      "start_at":1485273600000,
      "clicks":0,
      "created_at":1477029059253,
      "ctr":null,
      "placement_state":0,
      "publisher_name":"test 2",
      "seller_revenue_share":0.0,
      "requests":0,
      "ssp_platform_ecpc":null,
      "end_at":1485313200000,
      "publisher_ecpc":null,
      "placement_id":"63",
      "placement_name":"test_placement"
    }
  ],
  "summary": {
    "impressions":0,
    "publisher_revenue":0.0,
    "ssp_platform_ecpm":null,
    "exchange_rate_markup":0.0,
    "blank_impressions":0,
    "publisher_ecpm":null,
    "kept_impressions":0,
    "resold_impressions":0,
    "ssp_platform_profit":0.0,
    "fill_rate":null,
    "trade_logs":0,
    "amount":0.0,
    "ssp_platform_revenue":0.0,
    "default_impressions":0,
    "clicks":0,
    "ctr":null,
    "seller_revenue_share":0.0,
    "requests":0,
    "ssp_platform_ecpc":null,
    "publisher_ecpc":null
  },
  "meta": { "total": 1 }
}
```

### HTTP Request

`GET http://HOST/api/publishers/:publisher_id/placement_groups/:placement_group_id/placements`

### Query Parameters

Key | Required | Default | Type | Description
----| -------- | ------- | ---  | -------------
publisher_id | true | None | string | ID of Publisher
platform_id | true | 0 | string | ID of platform, also known as 'SSP Id'
placement_group_id | true | None | string | ID of Placement Groups
placement_ids | false | None | string | ID of Placements
state | false | 0 | string | states, eg: 0,1,2
keyword | false | None | string | keyword for Placement name
start_at | false | 0 | string | Start At, unix timestamp at milliseconds
end_at | false | None | string | End At, unix timestamp at milliseconds
order | false | placement_ids,desc;start_at,desc | string | Order. eg: requests,desc;ctr,asc. supported ordering fields: "start_at", "requests", "clicks", "impressions", "effective_impressions", "blank_impressions", "default_impressions", "psa_impressions", "kept_impressions", "resold_impressions", "rtb_impressions", "external_impression_impressions", "external_click_impressions", "cpm_bids", "cpc_bids", "cpa_bids", "amount", "exchange_rate_markup", "seller_revenue_share", "Placement_revenue", "ssp_platform_revenue", "ssp_platform_profit", "fill_rate", "ctr", "Placement_ecpm", "Placement_ecpc", "ssp_platform_ecpm", "ssp_platform_ecpc", "placement_id", "placement_group_id", "placement_name", "placement_state", "placements_count", "placement_created_at"
interval | false | summation | string | Interval
include_empty_row | false | 0 | long | 0 for false, 1 for true
offset | false | 0 | long | Offset
limit | false | 25 | long | Limit
currency | false | JPY | string | Currency. Support: USD,CNY,JPY,TWD,HKD
timezone | false | Asia/Shanghai | string | Timezone, eg: Asia/Shanghai

## Create a Placement

> Example Request:

```shell
curl -H "X-Requested-With: XMLHttpRequest" \
     -H "x-access-token: TOKEN" \
     -X POST \
     --data "placement[name]=name" \
     http://HOST/api/publishers/:publisher_id/placement_groups/:placment_group_id/placements
```

> Example Response:

```json
// 201
```

### HTTP Request
`POST http://HOST/api/publishers/:publisher_id/placements`

### Query Parameters

Parameter | Required | Default | Description
--------- | -------- | ------- | -----------
publisher_id | true | None |
placement_group_id | true | None |
placement | true | None | PlacementDAO

#### PlacementDAO

Key | Required | Type | Description
--------- | -------- | ------- | -----------
name | true | string |
state | true | ENUM | 0 - ACTIVE, 1 - INACTIVE, 2 - DELETED
has_reserve_price | false | integer | 1 or 0
cpm_price | false | float |
width | false |integer |
height | false | integer |
size | false | string | 200x100 . it is required for placements whose media type is banner
position | false | string | requisite for video. Available values: any / pre_roll / mid_roll / post_roll
max_duration | false | int | requisite for video
skippable | false | bool | requisite for video
media_type | false | string | banner / interstitial / native / video

# Placement Groups
## Get All Placement Groups

> Example Request:

```shell
curl -H "X-Requested-With: XMLHttpRequest" \
     -H "x-access-token: TOKEN" \
     http://HOST/api/publishers/:publisher_id/placement_groups
```

> Example Response:

```json
{
  "data": [
    {
      "id": 1,
      "name": "name",
      "publisher_id": 1,
      "url": "url",
      "description": "description",
      "universal_categories": {},
      "categories_data": [],
      "placements_count": 0
    }
  ],
  "meta": {
    "total": 1
  }
}
```

### HTTP Request
`GET http://HOST/api/publishers/:publisher_id/placement_groups`

### Query Parameters

Parameter | Required | Default | Description
--------- | -------- | ------- | -----------
publisher_id | true | None |
order | false | id,desc | `<column>,<asc or desc>`, columns could be: id, publisher_id, name, url, description, state, updated_at, placements_count

## Get a Specific Placement Group

> Example Request:

```shell
curl -H "X-Requested-With: XMLHttpRequest" \
     -H "x-access-token: TOKEN" \
     http://HOST/api/publishers/:publisher_id/placement_groups/:placment_group_id
```

> Example Response:

```json
{
  "id": 1,
  "name": "name",
  "publisher_id": 1,
  "url": "url",
  "description": "description",
  "universal_categories": {},
  "categories_data": [],
  "placements_count": 0
}
```

### HTTP Request
`GET http://HOST/api/publishers/:publisher_id/placement_groups/:placment_group_id`

### Query Parameters

Parameter | Required | Default | Description
--------- | -------- | ------- | -----------
publisher_id | true | None |
placement_group_id | true | None |

## Create a Placement Group

> Example Request:

```shell
curl -H "X-Requested-With: XMLHttpRequest" \
     -H "x-access-token: TOKEN" \
     --data "name=name"
     -X POST
     http://HOST/api/publishers/:publisher_id/placement_groups
```

> Example Response:

```json
{
  "id": 1,
  "name": "name",
  "publisher_id": 1,
  "url": "url",
  "description": "description",
  "universal_categories": {},
  "categories_data": [],
  "placements_count": 0
}
```

### HTTP Request
`POST http://HOST/api/publishers/:publisher_id/placement_groups`

### Query Parameters

Parameter | Required | Default | Description
--------- | -------- | ------- | -----------
publisher_id | true | None |
placement_group_id | true | None |
PlacementGroupDAO | true | None |

#### PlacementGroupDAO

Key | Required | Type | Description
--------- | -------- | ------- | -----------
name | true | string |
state | true | ENUM | 0 - ACTIVE, 2 - DELETED
url | false | string |
description | false | string |
universal_categories | false | string | json hash

## Update a Specific Placement Group or Batch Update Placement Groups

> Example Request:

```shell
curl -H "X-Requested-With: XMLHttpRequest" \
     -H "x-access-token: TOKEN" \
     --data "name=name"
     -X PUT
     http://HOST/api/publishers/:publisher_id/placement_groups/:placment_group_id
```

> Example Response:

```json
// 204
```

### HTTP Request
`PUT http://HOST/api/publishers/:publisher_id/placement_groups/:placment_group_id`

### Query Parameters

Parameter | Required | Default | Description
--------- | -------- | ------- | -----------
publisher_id | true | None |
placement_group_id | true | None |
PlacementGroupDAO | true | None |

#### PlacementGroupDAO

Key | Required | Type | Description
--------- | -------- | ------- | -----------
name | false | string |
state | false | ENUM | 0 - ACTIVE, 2 - DELETED
url | false | string |
description | false | string |
universal_categories | false | string | json hash

# Reports

## Get Recent Reports

> Example Request:

```shell
curl -H "X-Requested-With: XMLHttpRequest" \
     -H "x-access-token: TOKEN" \
    http://HOST/api/report_requests/recent_list
```

> Example Response:
```json
{
  "data": [
    {
      "id": 1,
      "name": "name",
      "range_type": "custom",
      "start_at": 1486101729,
      "end_at": 1486102729,
      "publisher_id": 2,
      "generate_status": "processing",
      "regular_report_frequency": "daily",
      "report_request_status": "enabled",
      "tz_name": "Europe/London"
    }
  ],
  "meta": { "total": 1 }
}
```

### HTTP Request
`GET http://HOST/api/report_requests/recent_list`

### Query Parameters

Parameter    | Required | Default | Type |  Description
------------ | -------- | ------- | ---- |  -----------
limit | false | 25 | int | limit per page
offset | false | 0 | int | if offset is set to N, first N records will be ignored
order | false | None | string | e.g.: name,desc, type,asc. supported ordering fields: id, name, type, publisher_id, report_type, range_type, start_at, end_at, interval, currency, filter_type, show_type, export_format, export_email, regular_export_format, regular_export_email, regular_report_frequency, generated_at, summary, generate_status, created_at, updated_at, send_at, is_rerun, creator_id

## Get Scheduled Reports

> Example Request:

```shell
curl -H "X-Requested-With: XMLHttpRequest" \
     -H "x-access-token: TOKEN" \
    http://HOST/api/report_requests/schedule_list
```

> Example Response:
```json
{
  "data": [
    {
      "id": 1,
      "name": "name",
      "range_type": "custom",
      "start_at": 1486101729,
      "end_at": 1486102729,
      "publisher_id": 2,
      "generate_status": "processing",
      "regular_report_frequency": "daily",
      "report_request_status": "enabled",
      "tz_name": "Europe/London"
    }
  ],
  "meta": { "total": 1 }
}
```

### HTTP Request
`GET http://HOST/api/report_requests/schedule_list`

### Query Parameters

Parameter    | Required | Default | Type |  Description
------------ | -------- | ------- | ---- |  -----------
limit | false | 25 | int | limit per page
offset | false | 0 | int | if offset is set to N, first N records will be ignored
order | false | None | string | e.g.: name,desc, type,asc. supported ordering fields: id, name, type, publisher_id, report_type, range_type, start_at, end_at, interval, currency, filter_type, show_type, export_format, export_email, regular_export_format, regular_export_email, regular_report_frequency, generated_at, summary, generate_status, created_at, updated_at, send_at, is_rerun, creator_id

## Get a Specific Report

> Example Request:

```shell
curl -H "X-Requested-With: XMLHttpRequest" \
     -H "x-access-token: TOKEN" \
    http://HOST/api/report_requests/:id
```

> Example Response:
```json
{
  "id": 1,
  "name": "name",
  "range_type": "yesterday",
  "start_at": 1486104005,
  "end_at": 1486104905,
  "publisher_id": 2,
  "generate_status": "processing",
  "type": "ScheduleReport",
  "show_type": "email",
  "interval": "summation",
  "currency": "USD",
  "export_format": "csv",
  "export_email": "recipient@mail.com",
  "regular_export_format": "recipient@mail.com",
  "regular_report_frequency": "daily",
  "placement_ids": [1, 2, 3],
  "placement_group_ids": [1],
  "placement_data": [{ "id": 1, "name": "hmm" }, { "id": 2, "name": "hmm" }, { "id": 3, "name": "hmm" }],
  "placement_group_data": [{ "id": 1, "name": "hmm" }],
  "timezone": {
    "id": 1,
    "short": "Europe/London",
    "long": "(UTC+00) Europe/London",
    "system": "Europe/London",
    "utc_offset": 0
  },
  "scheduled": true,
  "has_name": true,
  "filter_type": "filter_by_publisher",
  "selected_ids": [1]
}
```

### HTTP Request
`GET http://HOST/api/report_requests/:id`

### Query Parameters

Parameter | Required | Default | Description
--------- | -------- | ------- | -----------
id | true | None |

## Get the Review of a Specific Report

> Example Request:

```shell
curl -H "X-Requested-With: XMLHttpRequest" \
     -H "x-access-token: TOKEN" \
    http://HOST/api/report_requests/:id/review
```

> Example Response:
```json
{
  "data": [
    {
      "id": 1,
      "name": "name",
      "range_type": "yesterday",
      "start_at": 1486104005,
      "end_at": 1486104905,
      "publisher_id": 2,
      "generate_status": "processing"
    }
  ],
  "meta": {
    "summary": { "clicks": 12 },
    "currency": "USD",
    "timezone": {
      "id": 1,
      "short": "Europe/London",
      "long": "(UTC+00) Europe/London",
      "system": "Europe/London",
      "utc_offset": 0
    },
    "report_name": "report_name",
    "columns": ["clicks"],
    "total": 1
  }
}
```

> If you prefer a xlsx file:

```shell
curl -H "X-Requested-With: XMLHttpRequest" \
     -H "x-access-token: TOKEN" \
    http://HOST/api/report_requests/:id/review?format=xlsx
```

### HTTP Request
`GET http://HOST/api/report_requests/:id/review`

### Query Parameters

Parameter | Required | Default | Description
--------- | -------- | ------- | -----------
id | true | None |

## Create a New Report

> Example Request:

```shell
curl -H "X-Requested-With: XMLHttpRequest" \
     -H "x-access-token: TOKEN" \
    -X POST \
    --data "report_reqeust[name]=name" \
    http://HOST/api/report_requests
```

> Example Response:
```js
// Status code 201
```

### HTTP Request

`POST http://HOST/api/report_requests`

### Query Parameters

Parameter | Required| Type | Description
--------- | ------- | ---- | -----------
report_request | true    | ReportRequestDAO

#### ReportRequestDAO
Key | Required | Type | Description
--- | ----- | --- | ---
publisher_id | true | int |
range_type | true | string | supported values: 'custom', 'today', 'yesterday', 'this_month', 'last_month'. "start_at" and "end_at" are required only when the "range_type" is set to "custom"
currency | true | string | support: USD,CNY,JPY,TWD,HKD
timezone_id | true | int | support: please check out [timezone mapping](#timezone_mappings)
export_format | true | string | supported: "excel", "csv"
regular_export_format | true | string | supported: "regular_excel", "regular_csv"
regular_report_frequency | true | string | supported: "daily", "weekly", "monthly"
has_name | false | string | when it is set, the report to be craeted will adopt the value of "name" field
name | false | string | name of the report, it is required when "has_name" is set
filter_type | false | string | supported: "filter_by_publisher", "filter_by_placement", "filter_by_placement_group"
placement_ids | false | string | if you have multi ids, separtate them with ",", e.g.: "1,2,3"
placement_group_ids | false | string | if you have multi ids, separtate them with ",", e.g.: "1,2,3"
scheduled | false | string | set it to "1" if you'd like to create a scheduled report
regular_export_email | false | string | email address, it is required only when "scheduled" is set to "1"
show_type | false | string | supported values: "screen" and "email". By default, it is "screen", when it is set to "email" , "export_email" will become required
export_email | false | string | email address, it is required when "show_type" is set to "email"
start_at | false | int | timestamp in seconds. required only when "range_type" is set to "custom"
end_at | false | int | timestamp in seconds. required only when "range_type" is set to "custom"
interval | false | string | supported values: "summation", "hour", "day", "month". By default, it is "summation"

## Update a Specific Report

> Example Request:

```shell
curl -H "X-Requested-With: XMLHttpRequest" \
     -H "x-access-token: TOKEN" \
    -X PUT \
    --data "report_reqeust[name]=name" \
    http://HOST/api/report_requests/:id
```

> Example Response:
```js
// Status code 204
```

### HTTP Request

`PUT http://HOST/api/report_requests/:id`

### Query Parameters

Parameter | Required| Type | Description
--------- | ------- | ---- | -----------
report_request | true    | ReportRequestDAO

#### ReportRequestDAO
Key | Required | Type | Description
--- | ----- | --- | ---
publisher_id | true | int |
range_type | true | string | supported values: 'custom', 'today', 'yesterday', 'this_month', 'last_month'. "start_at" and "end_at" are required only when the "range_type" is set to "custom"
currency | true | string | support: USD,CNY,JPY,TWD,HKD
timezone_id | true | int | support: please check out [timezone mapping](#timezone_mappings)
export_format | true | string | supported: "excel", "csv"
regular_export_format | true | string | supported: "regular_excel", "regular_csv"
regular_report_frequency | true | string | supported: "daily", "weekly", "monthly"
has_name | false | string | when it is set, the report to be craeted will adopt the value of "name" field
name | false | string | name of the report, it is required when "has_name" is set
filter_type | false | string | supported: "filter_by_publisher", "filter_by_placement", "filter_by_placement_group"
placement_ids | false | string | if you have multi ids, separtate them with ",", e.g.: "1,2,3"
placement_group_ids | false | string | if you have multi ids, separtate them with ",", e.g.: "1,2,3"
scheduled | false | string | set it to "1" if you'd like to create a scheduled report
regular_export_email | false | string | email address, it is required only when "scheduled" is set to "1"
show_type | false | string | supported values: "screen" and "email". By default, it is "screen", when it is set to "email" , "export_email" will become required
export_email | false | string | email address, it is required when "show_type" is set to "email"
start_at | false | int | timestamp in seconds. required only when "range_type" is set to "custom"
end_at | false | int | timestamp in seconds. required only when "range_type" is set to "custom"
interval | false | string | supported values: "summation", "hour", "day", "month". By default, it is "summation"

## Delete a Specific Report

> Example Request:

```shell
curl -H "X-Requested-With: XMLHttpRequest" \
     -H "x-access-token: TOKEN" \
    -X DELETE \
    http://HOST/api/report_requests/:id
```

> Example Response:
```js
// Status code 204
```

### HTTP Request

`DELETE http://HOST/api/report_requests/:id`

### Query Parameters

Parameter | Required| Type | Description
--------- | ------- | ---- | -----------
id | true | int |

## Rerun a Specific Report

> Example Request:

```shell
curl -H "X-Requested-With: XMLHttpRequest" \
     -H "x-access-token: TOKEN" \
    -X POST \
    http://HOST/api/report_requests/:id/rerun
```

> Example Response:
```js
// Status code 201
```

### HTTP Request

`POST http://HOST/api/report_requests/:id/rerun`

### Query Parameters

Parameter | Required| Type | Description
--------- | ------- | ---- | -----------
id | true | int |

# Timezone Mappings
<a name="timezone_mappings"></a>

ID | Name
--- | -----
1 | Europe/London
2 | GMT
3 | Europe/Berlin
4 | Asia/Jerusalem
6 | Europe/Moscow
7 | Asia/Dubai
11 | Indian/Maldives
12 | Asia/Dhaka
15 | Asia/Bangkok
16 | Asia/Ho Chi Minh
17 | Asia/Jakarta
18 | Asia/Hong Kong
19 | Asia/Macau
20 | Asia/Beijing
21 | Asia/Singapore
22 | Asia/Taipei
24 | Asia/Seoul
25 | Asia/Tokyo
27 | Asia/Magadan
28 | Australia/Sydney
29 | Asia/Sakhalin
30 | America/Scoresbysund
31 | Atlantic/South Georgia
32 | America/Argentina/Buenos Aires
35 | America/Halifax
36 | America/New York
37 | US/Eastern
38 | America/Chicago
39 | US/Central
40 | America/Denver
41 | US/Mountain
42 | America/Los Angeles
43 | US/Pacific
44 | America/Juneau
45 | US/Hawaii
