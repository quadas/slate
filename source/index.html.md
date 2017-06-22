---
title: Quadas API Reference

language_tabs:
  - shell

toc_footers:

includes:
  - timezones
  - countries
  - universal_categories
  - errors

search: false
---

# Introduction

Welcome to the Publisher API! You can use our API to access Publisher API endpoints, which can CRUD your owned publishers. The API is organized around REST. Our API has predictable, resource-oriented URLs, and uses HTTP response codes to indicate API errors. We use built-in HTTP features, like HTTP authentication and HTTP verbs, which are understood by off-the-shelf HTTP clients.

# Access Token

Please retrieve your own token before accessing other resources.

> Example Request:

```shell
curl --data "username=USERNAME&password=PASSWORD" \
  --referer http://UI_HOST \
  -X POST http://HOST/api/idp/sessions
```

> Example Response:

```js
// You'll notice that the response consists of: "eyJ0eXAi..." + "|" + "eyJ0eX..."
// The former part is checksum, the latter is access token which will be required in other requests
{ "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJwbGF0Zm9ybV9pZCI6IjEyIiwiZW1haWwiOiJ4QHkuY29tIiwidXNlcm5hbWUiOiJzdXBlcmFkbWluIiwiY3VycmVuY3kiOiJDTlkiLCJsYW5ndWFnZSI6ImNuIiwiZXhwaXJlc19hdCI6MTQ5Nzg2NDk3OCwicm9sZXMiOlsiU3VwZXIgQWRtaW4iXSwidGltZXpvbmUiOnsiaWQiOiIyMiIsInV0Y19vZmZzZXQiOjQ4MCwibG9uZyI6IihVVEMrMDgpIEFzaWEgLyBUYWlwZWkiLCJzeXN0ZW0iOiJBc2lhL1RhaXBlaSJ9fQ.h3kvM0ASi6MOx2hid3xT4xRCZRCSG8onWjUfO7hd09Q|eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJwbGF0Zm9ybV9pZCI6IjEyIiwidXNlcm5hbWUiOiJzdXBlcmFkbWluIiwidG9rZW4iOiJkMjgxYzc2MTYxNGRmOTgxNWJmOTJhYzdmODFiOWRlNWRhODZiZDI5MDUzZTNjNDY3MzdmNjhjODU2ODJhN2NkIn0.PA9O34LmRMx5CBdm-N4j0qOpjgLtDEsKgzNuUVSIve0" }
```

### HTTP Request

`POST http://HOST/api/idp/sessions`


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
  -H x-access-token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJwbGF0Zm9ybV9pZCI6IjEyIiwidXNlcm5hbWUiOiJzdXBlcmFkbWluIiwidG9rZW4iOiIxMDU1M2ZjZTk0ZjE2YmQ5NGJmNWZjZTZjNzJjYTVkOTQwNjY2N2QwNmI0NWQ4OWE0MTc3OGYwMDFlOTA5MWNiIn0.fMZy0m0J6yaTQabbF9LCQmgdV0ujF1wfthCKmELhiIs \
  http://HOST/api/publishers
```

To authorize, just inject the pairs below into your request header:

- `X-Requested-With: XMLHttpRequest`
- `x-access-token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJwbGF0Zm9ybV9pZCI6IjEyIiwidXNlcm5hbWUiOiJzdXBlcmFkbWluIiwidG9rZW4iOiIxMDU1M2ZjZTk0ZjE2YmQ5NGJmNWZjZTZjNzJjYTVkOTQwNjY2N2QwNmI0NWQ4OWE0MTc3OGYwMDFlOTA5MWNiIn0.fMZy0m0J6yaTQabbF9LCQmgdV0ujF1wfthCKmELhiIs`

<aside class="notice">
You must replace value of `x-access-token` with your own access token.
</aside>

# Publishers

## Get All Publishers

> Example Request:

```shell
curl -H "X-Requested-With: XMLHttpRequest" \
     -H "x-access-token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJwbGF0Zm9ybV9pZCI6IjEyIiwidXNlcm5hbWUiOiJzdXBlcmFkbWluIiwidG9rZW4iOiIxMDU1M2ZjZTk0ZjE2YmQ5NGJmNWZjZTZjNzJjYTVkOTQwNjY2N2QwNmI0NWQ4OWE0MTc3OGYwMDFlOTA5MWNiIn0.fMZy0m0J6yaTQabbF9LCQmgdV0ujF1wfthCKmELhiIs" \
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

The newly created publisher may not be to be observed immediately via this API.
For more detail, please check out section "Create a Publisher".

### Query Parameters

Parameter    | Required | Default | Type |  Description
------------ | -------- | ------- | ---- |  -----------
state | false | 0 | string | states, accepted values: 0 - active; 1 - inactive; 0,1 - all
keyword | false | None | string | keyword for publisher name
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
     -H "x-access-token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJwbGF0Zm9ybV9pZCI6IjEyIiwidXNlcm5hbWUiOiJzdXBlcmFkbWluIiwidG9rZW4iOiIxMDU1M2ZjZTk0ZjE2YmQ5NGJmNWZjZTZjNzJjYTVkOTQwNjY2N2QwNmI0NWQ4OWE0MTc3OGYwMDFlOTA5MWNiIn0.fMZy0m0J6yaTQabbF9LCQmgdV0ujF1wfthCKmELhiIs" \
     http://HOST/api/publishers/1
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

`GET http://HOST/api/publishers/{PUBLISHER_ID}`

## Create a Publisher

> Example Request with eager load enabled:

```shell
# with
curl -H "X-Requested-With: XMLHttpRequest" \
     -H "x-access-token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJwbGF0Zm9ybV9pZCI6IjEyIiwidXNlcm5hbWUiOiJzdXBlcmFkbWluIiwidG9rZW4iOiIxMDU1M2ZjZTk0ZjE2YmQ5NGJmNWZjZTZjNzJjYTVkOTQwNjY2N2QwNmI0NWQ4OWE0MTc3OGYwMDFlOTA5MWNiIn0.fMZy0m0J6yaTQabbF9LCQmgdV0ujF1wfthCKmELhiIs" \
     -H "Content-Type: application/json" \
     --data {\"eager_load\":1,\"publisher\":{\"name\":\"createdviaapi-c\",\"username\":\"createdapic\",\"email\":\"api@api.com\",\"state\":\"inactive\",\"cpm_deal\":1,\"currency\":\"USD\",\"country_id\":\"Hong Kong\",\"payment_term_attributes\":{\"pricing_type\":4,\"cpm_price\":2}}} \
     -X POST \
     http://HOST/api/publishers
```

> Example Response(200):

```json
{
  "data": {
    "id": 33,
    "name": "createdviaapi-d",
    "state": "inactive",
    "currency": "USD",
    "placements_count": 0,
    "payment_term": {
      "id": 35,
      "publisher_id": 33,
      "pricing_type": "cpm",
      "cpm_price": 2.0,
      "revenue_share_rate": null,
      "revenue_share_rate_percentage": null,
      "apply_served": false
    }
  }
}
```

> Example Request:

```shell
curl -H "X-Requested-With: XMLHttpRequest" \
     -H "Content-Type: application/json" \
     -H "x-access-token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJwbGF0Zm9ybV9pZCI6IjEyIiwidXNlcm5hbWUiOiJzdXBlcmFkbWluIiwidG9rZW4iOiIxMDU1M2ZjZTk0ZjE2YmQ5NGJmNWZjZTZjNzJjYTVkOTQwNjY2N2QwNmI0NWQ4OWE0MTc3OGYwMDFlOTA5MWNiIn0.fMZy0m0J6yaTQabbF9LCQmgdV0ujF1wfthCKmELhiIs" \
     --data "{\"publisher\":{\"name\":\"createdviaapi\",\"username\":\"createdapi\",\"email\":\"api@api.com\",\"state\":0,\"cpm_deal\":1,\"currency\":\"USD\",\"country_id\":\"Hong Kong\",\"payment_term_attributes\":{\"pricing_type\":4,\"cpm_price\":2}}}" \
     -X POST \
     http://HOST/api/publishers
```

> Example Response:

```json
{}
```

### HTTP Request

`POST http://HOST/api/publishers`

It's an async API, whereby the new record cannot be seen until it gets indexed.
But if you want to retrieve the record as soon as the API responds, please append `eager_load=1` to your request param.

### Query Parameters

Parameter | Required| Type | Description
--------- | ------- | ---- | -----------
eager_load | false | None | set it to "1" if you prefer 200 response with data rather than plain 201 status code
publisher | true    | PublisherDAO

#### PublihserDAO
Key | Required | Type | Description
--- | ----- | --- | ---
name | true | string |
username | true | string |
state | true | string | accepted values: active, inactive
currency | true | string | USD,CNY,JPY,TWD,HKD
country_id | true | string | valid country id, checkout [country mapping](#country-mappings)
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

```shell
curl -H "X-Requested-With: XMLHttpRequest" \
     -H "x-access-token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJwbGF0Zm9ybV9pZCI6IjEyIiwidXNlcm5hbWUiOiJzdXBlcmFkbWluIiwidG9rZW4iOiIxMDU1M2ZjZTk0ZjE2YmQ5NGJmNWZjZTZjNzJjYTVkOTQwNjY2N2QwNmI0NWQ4OWE0MTc3OGYwMDFlOTA5MWNiIn0.fMZy0m0J6yaTQabbF9LCQmgdV0ujF1wfthCKmELhiIs" \
     -H "Content-Type: application/json" \
     --data "{\"publisher\":{\"name\":\"editedviaapi\",\"email\":\"edited@mail.com\",\"state\":"active",\"cpm_deal\":1,\"currency\":\"USD\",\"country_id\":\"Hong Kong\",\"payment_term_attributes\":{\"pricing_type\":5,\"revenue_share_rate\":2.3,\"revenue_share_rate_percentage\":0.2}}}" \
     -X POST \
     http://HOST/api/publishers/1,2
```

> Example Response:

```json
{}
```

### HTTP Request

`POST http://HOST/api/publishers/{PUBLISHER_IDS_SEPARATED_WITH_COMMA}`

### Query Parameters

Parameter | Required| Type | Description
--------- | ------- | ---- | -----------
publisher | true    | PublisherDAO |

#### PublihserDAO
Key | Required | Type | Description
--- | ----- | --- | ---
name | false | string |
state | false | string | accepted values: active, inactive
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
     -H "x-access-token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJwbGF0Zm9ybV9pZCI6IjEyIiwidXNlcm5hbWUiOiJzdXBlcmFkbWluIiwidG9rZW4iOiIxMDU1M2ZjZTk0ZjE2YmQ5NGJmNWZjZTZjNzJjYTVkOTQwNjY2N2QwNmI0NWQ4OWE0MTc3OGYwMDFlOTA5MWNiIn0.fMZy0m0J6yaTQabbF9LCQmgdV0ujF1wfthCKmELhiIs" \
     -H "Content-Type: application/json" \
     --data "{\"placement_group_id\":\"53\",\"state\":"active",\"keyword\":\"as\",\"order\":\"start_at,desc\",\"currency\":\"JPY\"}" \
     http://HOST/api/publishers/29/placements
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
      "placement_id":"53",
      "placement_name":"teast_placement"
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

`GET http://HOST/api/publishers/{PUBLISHER_ID}/placements`

The newly created placement may not be to be observed immediately via this API.
For more detail, please check out section "Create a Placement".

### Query Parameters

Key | Required | Default | Type | Description
----| -------- | ------- | ---  | -------------
placement_group_id | false | None | string | ID of Placement Groups, e.g.: "53"
state | false | 0 | string | accepted values: 0 - active; 1 - inactive; 0,1 - all
keyword | false | None | string | keyword for Placement name
start_at | false | 0 | string | Start At, unix timestamp at milliseconds
end_at | false | None | string | End At, unix timestamp at milliseconds
order | false | placement_ids,desc;start_at,desc | string | Order. eg: requests,desc;ctr,asc. supported ordering fields: "start_at", "requests", "clicks", "impressions", "effective_impressions", "blank_impressions", "default_impressions", "psa_impressions", "kept_impressions", "resold_impressions", "rtb_impressions", "external_impression_impressions", "external_click_impressions", "cpm_bids", "cpc_bids", "cpa_bids", "amount", "exchange_rate_markup", "seller_revenue_share", "Placement_revenue", "ssp_platform_revenue", "ssp_platform_profit", "fill_rate", "ctr", "Placement_ecpm", "Placement_ecpc", "ssp_platform_ecpm", "ssp_platform_ecpc", "placement_id", "placement_group_id", "placement_name", "placement_state", "placements_count", "placement_created_at"
offset | false | 0 | long | Offset
limit | false | 25 | long | Limit
currency | false | JPY | string | Currency. Support: USD,CNY,JPY,TWD,HKD
timezone | false | Asia/Shanghai | string | Timezone, eg: Asia/Shanghai

## Get a Specific Placement

> Example Request:

```shell
curl -H "X-Requested-With: XMLHttpRequest" \
     -H "x-access-token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJwbGF0Zm9ybV9pZCI6IjEyIiwidXNlcm5hbWUiOiJzdXBlcmFkbWluIiwidG9rZW4iOiIxMDU1M2ZjZTk0ZjE2YmQ5NGJmNWZjZTZjNzJjYTVkOTQwNjY2N2QwNmI0NWQ4OWE0MTc3OGYwMDFlOTA5MWNiIn0.fMZy0m0J6yaTQabbF9LCQmgdV0ujF1wfthCKmELhiIs" \
     http://HOST/api/publishers/29/placement_groups/53/placements/1
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
`GET http://HOST/api/publishers/{PUBLISHER_ID}/placement_groups/{PLACMENT_GROUP_ID}/placements/{PLACEMENT_ID}`

## Duplicate Placements

> Example Request:

```shell
curl -H "X-Requested-With: XMLHttpRequest" \
     -H "x-access-token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJwbGF0Zm9ybV9pZCI6IjEyIiwidXNlcm5hbWUiOiJzdXBlcmFkbWluIiwidG9rZW4iOiIxMDU1M2ZjZTk0ZjE2YmQ5NGJmNWZjZTZjNzJjYTVkOTQwNjY2N2QwNmI0NWQ4OWE0MTc3OGYwMDFlOTA5MWNiIn0.fMZy0m0J6yaTQabbF9LCQmgdV0ujF1wfthCKmELhiIs" \
     -H "Content-Type: application/json" \
     --data "{\"placements\":[{\"placement_id\":114,\"name\":\"copy aa\"}]}" \
     -X POST \
     http://HOST/api/publishers/29/placements/duplicate
```

> Example Response:

```
HTTP status code 201
```

### HTTP Request
`POST http://HOST/api/publishers/{PUBLISHER_ID}/placements/duplicate`

### Query Parameters

Parameter | Required | Default | Description
--------- | -------- | ------- | -----------
placements | true | None |

#### PlacementDuplicateDAO

Key | Required | Default | Description
--------- | -------- | ------- | -----------
placement_id | true | None |
name | true | None |

## Update a Specific Placements or Batch Update Placements

> Example Request:

```shell
curl -H "X-Requested-With: XMLHttpRequest" \
     -H "x-access-token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJwbGF0Zm9ybV9pZCI6IjEyIiwidXNlcm5hbWUiOiJzdXBlcmFkbWluIiwidG9rZW4iOiIxMDU1M2ZjZTk0ZjE2YmQ5NGJmNWZjZTZjNzJjYTVkOTQwNjY2N2QwNmI0NWQ4OWE0MTc3OGYwMDFlOTA5MWNiIn0.fMZy0m0J6yaTQabbF9LCQmgdV0ujF1wfthCKmELhiIs" \
     -H "Content-Type: application/json" \
     --data "{\"placement\":{\"name\":\"another_name\",\"state\":1,\"media_type\":\"Video\",\"has_reserve_price\":\"1\",\"reserve_cpm\":1.2,\"size\":\"3x3\",\"position\":\"pre_roll\",\"max_duration\":30,\"skippable\":true,\"universal_categories\":\"{\\"3\\": [57] }\",\"custom_categories\":\"[{\\"prop_id\\":1,\\"name\\":\\"Cat\\",\\"value\\":\\"identical_value\\",\\"disable\\":false}]\",\"custom_tags\":\"[{\\"prop_id\\":1,\\"name\\":\\"Tag\\",\\"value\\":\\"identical_value\\",\\"disable\\":false}]\"}}" \
     http://HOST/api/publishers/29/placements/1
```

> Example Response:

```json
HTTP status code 204
```

### HTTP Request
`POST http://HOST/api/publishers/{PUBLISHER_ID}/placements/{PLACEMENT_ID_SEPARATED_WITH_COMMA}`

### Query Parameters

Parameter | Required | Default | Description
--------- | -------- | ------- | -----------
placement | true | None | PlacementDAO

#### PlacementDAO

Key | Required | Type | Description
--------- | -------- | ------- | -----------
name | false | string |
state | false | string | accepted values: active, inactive
media_type | false | string | banner / interstitial / native / video
has_reserve_price | false | string | "1" or "0", it is required to be "1" when reserve_cpm has any value
reserve_cpm | false | float |
size | false | string | "WIDTHxHEIGHT", e.g.: 200x100 . it is required for placements whose media type is banner
position | false | string | requisite for video. Available values: any / pre_roll / mid_roll / post_roll
max_duration | false | int | requisite for video
skippable | false | bool | requisite for video
universal_categories | false | string | json hash which follows a particular style "{ parent_id: [cat_a, cat_b] }", e.g.: "{ \"3\": [57, 58] }" stands for selecting categories whose id is 57 or 58, both of them shares a parent category whose id is 3. As for the universal category table, please check out the section "Universal Category"
custom_categories | false | string | json hash. e.g.: "[{ \"prop_id\": 1, \"name\": \"name\", \"value\": \"value\", \"disable\": true }]" stands for selecting the record that matches the given props among uploaded categories. As for how to upload, please check out the section "Custom Categories/Tags"
custom_tags | false | string | json hash.  e.g.: "[{ \"prop_id\": 1, \"name\": \"name\", \"value\": \"value\", \"disable\": true }]" stands for selecting the record that matches the given props among uploaded tags. As for how to upload, please check out the section "Custom Categories/Tags"

## Export Tag of a Specific Placement

> Example Request:

```shell
curl -H "X-Requested-With: XMLHttpRequest" \
     -H "x-access-token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJwbGF0Zm9ybV9pZCI6IjEyIiwidXNlcm5hbWUiOiJzdXBlcmFkbWluIiwidG9rZW4iOiIxMDU1M2ZjZTk0ZjE2YmQ5NGJmNWZjZTZjNzJjYTVkOTQwNjY2N2QwNmI0NWQ4OWE0MTc3OGYwMDFlOTA5MWNiIn0.fMZy0m0J6yaTQabbF9LCQmgdV0ujF1wfthCKmELhiIs" \
     http://HOST/api/publishers/1/placements/2/export_tag
```

> Example Response:

```json
{
  "placement_id": "1_2",
  "tag": "<div id=\"1_2\"></div><script>code here</script>"
}
```

### HTTP Request
`GET http://HOST/api/publishers/{PUBLISHER_ID}/placements/{PLACEMENT_ID}/export_tag`

## Create a Placement

> Example Request with eager load enabled:

```shell
# with
curl -H "X-Requested-With: XMLHttpRequest" \
     -H "x-access-token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJwbGF0Zm9ybV9pZCI6IjEyIiwidXNlcm5hbWUiOiJzdXBlcmFkbWluIiwidG9rZW4iOiIxMDU1M2ZjZTk0ZjE2YmQ5NGJmNWZjZTZjNzJjYTVkOTQwNjY2N2QwNmI0NWQ4OWE0MTc3OGYwMDFlOTA5MWNiIn0.fMZy0m0J6yaTQabbF9LCQmgdV0ujF1wfthCKmELhiIs" \
     -H "Content-Type: application/json" \
     --data {\"eager_load\":1,\"placement\":{\"name\":\"x_name_1\",\"placement_group_id\":40,\"state\":1,\"media_type\":\"Video\",\"has_reserve_price\":\"1\",\"reserve_cpm\":1.2,\"size\":\"3x3\",\"position\":\"pre_roll\",\"max_duration\":30,\"skippable\":true,\"universal_categories\":\"{ \\"3\\": [57] }\",\"custom_categories\":\"[{\\"prop_id\\":1,\\"name\\":\\"Cat\\",\\"value\\":\\"identical_value\\",\\"disable\\":false}]\",\"custom_tags\":\"[{\\"prop_id\\":1,\\"name\\":\\"Tag\\",\\"value\\":\\"identical_value\\",\\"disable\\":false}]\"}} \
     -X POST \
     http://HOST/api/publishers/29/placement_groups/53/placements
```

> Example Response(200):

```json
{
  "data": {
    "id": "124",
    "name": "x_name_2",
    "state": "inactive",
    "size": null,
    "media_type": "Video",
    "universal_categories": {
      "3": [
        57
      ]
    },
    "categories_data": [
      {
        "id": 3,
        "name": "Business",
        "children": [
          {
            "id": 57,
            "name": "Advertising"
          }
        ]
      }
    ],
    "placement_group_id": 40,
    "group_categories_data": [],
    "ucat_mode": "unknown",
    "ccat_mode": "unknown",
    "ctag_mode": "unknown",
    "position": "pre_roll",
    "max_duration": "30.0",
    "skippable": true,
    "custom_categories": [
      {
        "prop_id": 1,
        "name": "Cat",
        "value": "identical_value",
        "disable": false,
        "children": null
      }
    ],
    "custom_tags": [
      {
        "prop_id": 1,
        "name": "Tag",
        "value": "identical_value",
        "disable": false,
        "children": null
      }
    ],
    "group_custom_categories": [],
    "group_custom_tags": [],
    "metrics": {
      "publisher_state": 0,
      "impressions": 0,
      "publisher_revenue": 0.0,
      "ssp_platform_ecpm": null,
      "placements_count": 19,
      "exchange_rate_markup": 0.0,
      "blank_impressions": 0,
      "publisher_ecpm": null,
      "kept_impressions": 0,
      "resold_impressions": 0,
      "ssp_platform_profit": 0.0,
      "fill_rate": null,
      "publisher_id": 21,
      "placement_group_id": 40,
      "trade_logs": 0,
      "amount": 0.0,
      "ssp_platform_revenue": 0.0,
      "default_impressions": 0,
      "clicks": 0,
      "created_at": 1498130683000,
      "ctr": null,
      "placement_state": 1,
      "publisher_name": "Name",
      "seller_revenue_share": 0.0,
      "requests": 0,
      "ssp_platform_ecpc": null,
      "publisher_ecpc": null,
      "placement_id": 124,
      "placement_name": "x_name_2"
    }
  }
}
```

> Example Request:

```shell
curl -H "X-Requested-With: XMLHttpRequest" \
     -H "x-access-token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJwbGF0Zm9ybV9pZCI6IjEyIiwidXNlcm5hbWUiOiJzdXBlcmFkbWluIiwidG9rZW4iOiIxMDU1M2ZjZTk0ZjE2YmQ5NGJmNWZjZTZjNzJjYTVkOTQwNjY2N2QwNmI0NWQ4OWE0MTc3OGYwMDFlOTA5MWNiIn0.fMZy0m0J6yaTQabbF9LCQmgdV0ujF1wfthCKmELhiIs" \
     -H "Content-Type: application/json" \
    --data "{\"placement\":{\"name\":\"x_name\",\"placement_group_id\":53,\"state\":1,\"media_type\":\"Video\",\"has_reserve_price\":\"1\",\"reserve_cpm\":1.2,\"size\":\"3x3\",\"position\":\"pre_roll\",\"max_duration\":30,\"skippable\":true,\"universal_categories\":\"{ \\"3\\": [57] }\",\"custom_categories\":\"[{\\"prop_id\\":1,\\"name\\":\\"Cat\\",\\"value\\":\\"identical_value\\",\\"disable\\":false}]\",\"custom_tags\":\"[{\\"prop_id\\":1,\\"name\\":\\"Tag\\",\\"value\\":\\"identical_value\\",\\"disable\\":false}]\"}}" \
     -X POST \
     http://HOST/api/publishers/29/placement_groups/53/placements
```

> Example Response(201):

```
HTTP status code 201
```

### HTTP Request
`POST http://HOST/api/publishers/{PUBLISHER_ID}/placement_groups/{PLACEMENT_GROUP_ID}/placements`

It's an async API, whereby the new record cannot be seen until it gets indexed.
But if you want to retrieve the record as soon as the API responds, please append `eager_load=1` to your request param.

### Query Parameters

Parameter | Required | Default | Description
--------- | -------- | ------- | -----------
eager_load | false | None | set it to "1" if you prefer 200 response with data rather than plain 201 status code
placement | true | None | PlacementDAO

#### PlacementDAO

Key | Required | Type | Description
--------- | -------- | ------- | -----------
placement_group_id | true | None |
name | false | string |
state | false | string | accepted values: active, inactive
media_type | false | string | banner / interstitial / native / video
has_reserve_price | false | string | "1" or "0", it is required to be "1" when reserve_cpm has any value
reserve_cpm | false | float |
size | false | string | "WIDTHxHEIGHT", e.g.: 200x100 . it is required for placements whose media type is banner
position | false | string | requisite for video. Available values: any / pre_roll / mid_roll / post_roll
max_duration | false | int | requisite for video
skippable | false | bool | requisite for video
universal_categories | false | string | json hash which follows a particular style "{ parent_id: [cat_a, cat_b] }", e.g.: "{ \"3\": [57, 58] }" stands for selecting categories whose id is 57 or 58, both of them shares a parent category whose id is 3. As for the universal category table, please check out the section "Universal Category"
custom_categories | false | string | json hash. e.g.: "[{ \"prop_id\": 1, \"name\": \"name\", \"value\": \"value\", \"disable\": true }]" stands for selecting the record that matches the given props among uploaded categories. As for how to upload, please check out the section "Custom Categories/Tags"
custom_tags | false | string | json hash.  e.g.: "[{ \"prop_id\": 1, \"name\": \"name\", \"value\": \"value\", \"disable\": true }]" stands for selecting the record that matches the given props among uploaded tags. As for how to upload, please check out the section "Custom Categories/Tags"

# Placement Groups
## Get All Placement Groups

> Example Request:

```shell
curl -H "X-Requested-With: XMLHttpRequest" \
     -H "x-access-token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJwbGF0Zm9ybV9pZCI6IjEyIiwidXNlcm5hbWUiOiJzdXBlcmFkbWluIiwidG9rZW4iOiIxMDU1M2ZjZTk0ZjE2YmQ5NGJmNWZjZTZjNzJjYTVkOTQwNjY2N2QwNmI0NWQ4OWE0MTc3OGYwMDFlOTA5MWNiIn0.fMZy0m0J6yaTQabbF9LCQmgdV0ujF1wfthCKmELhiIs" \
     http://HOST/api/publishers/29/placement_groups
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
`GET http://HOST/api/publishers/{PUBLISHER_ID}/placement_groups`

### Query Parameters

Parameter | Required | Default | Description
--------- | -------- | ------- | -----------
order | false | id,desc | `<column>,<asc or desc>`, columns could be: id, publisher_id, name, url, description, state, updated_at, placements_count

## Get a Specific Placement Group

> Example Request:

```shell
curl -H "X-Requested-With: XMLHttpRequest" \
     -H "x-access-token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJwbGF0Zm9ybV9pZCI6IjEyIiwidXNlcm5hbWUiOiJzdXBlcmFkbWluIiwidG9rZW4iOiIxMDU1M2ZjZTk0ZjE2YmQ5NGJmNWZjZTZjNzJjYTVkOTQwNjY2N2QwNmI0NWQ4OWE0MTc3OGYwMDFlOTA5MWNiIn0.fMZy0m0J6yaTQabbF9LCQmgdV0ujF1wfthCKmELhiIs" \
     http://HOST/api/publishers/29/placement_groups/1
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
`GET http://HOST/api/publishers/{PUBLISHER_ID}/placement_groups/{PLACEMENT_GROUP_ID}`

## Create a Placement Group

> Example Request:

```shell
curl -H "X-Requested-With: XMLHttpRequest" \
     -H "x-access-token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJwbGF0Zm9ybV9pZCI6IjEyIiwidXNlcm5hbWUiOiJzdXBlcmFkbWluIiwidG9rZW4iOiIxMDU1M2ZjZTk0ZjE2YmQ5NGJmNWZjZTZjNzJjYTVkOTQwNjY2N2QwNmI0NWQ4OWE0MTc3OGYwMDFlOTA5MWNiIn0.fMZy0m0J6yaTQabbF9LCQmgdV0ujF1wfthCKmELhiIs" \
     --data "placment_group[name]=name"
     -X POST
     http://HOST/api/publishers/29/placement_groups
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
`POST http://HOST/api/publishers/{PUBLISHER_ID}/placement_groups`

### Query Parameters

Parameter | Type | Required | Default | Description
--------- | ---- | -------- | ------- | -----------
placement_group | PlacementGroupDAO | true | None |

#### PlacementGroupDAO

Key | Required | Type | Description
--------- | -------- | ------- | -----------
name | true | string |
state | true | string | accepted values: active, deleted
url | false | string |
description | false | string |
universal_categories | false | string | json hash which follows a particular style "{ parent_id: [cat_a, cat_b] }", e.g.: "{ \"3\": [57, 58] }" stands for selecting categories whose id is 57 or 58, both of them shares a parent category whose id is 3. As for the universal category table, please check out the section "Universal Category"
custom_categories | false | string | json hash e.g.: "[{ \"prop_id\": 1, \"name\": \"name\", \"value\": \"valcustom_tags | false | string | json hash.  e.g.: "[{ \"prop_id\": 1, \"name\": \"name\", \"value\": \"value\", \"disable\": true }]" stands for selecting the record that matches the given props among uploaded tags. As for how to upload, please check out the section "Custom Categories/Tags"ue\", \"disable\": true }]" stands for selecting the record that matches the given props among uploaded categories. As for how to upload, please check out the section "Custom Categories/Tags"

## Update a Specific Placement Group or Batch Update Placement Groups

> Example Request:

```shell
curl -H "X-Requested-With: XMLHttpRequest" \
     -H "x-access-token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJwbGF0Zm9ybV9pZCI6IjEyIiwidXNlcm5hbWUiOiJzdXBlcmFkbWluIiwidG9rZW4iOiIxMDU1M2ZjZTk0ZjE2YmQ5NGJmNWZjZTZjNzJjYTVkOTQwNjY2N2QwNmI0NWQ4OWE0MTc3OGYwMDFlOTA5MWNiIn0.fMZy0m0J6yaTQabbF9LCQmgdV0ujF1wfthCKmELhiIs" \
     -H "Content-Type: application/json" \
     --data "{\"placement_group\":{\"name\":\"updatedbyapi\",\"state\":\"deleted\",\"description\":\"asdsdA\",\"url\":\"http://google.com\",\"universal_categories\":\"{ \\"3\\": [57] }\"}}" \
     -X POST \
     http://HOST/api/publishers/29/placement_groups/1
```

> Example Response:

```
HTTP status code 204
```

### HTTP Request
`PUT http://HOST/api/publishers/{PUBLISHER_DI}/placement_groups/{PLACEMENT_GROUP_ID_SEPARATED_WITH_COMMA}`

If you'd like to update multi placement groups simultaneously, replace `{PLACEMENT_GROUP_ID_SEPARATED_WITH_COMMA}` with ids like "1,2,3".

### Query Parameters

Parameter | Type | Required | Default | Description
--------- | ---- | -------- | ------- | -----------
placement_group | PlacementGroupDAO | true | None |

#### PlacementGroupDAO

Key | Required | Type | Description
--------- | -------- | ------- | -----------
name | false | string |
state | false | string | accepted values: active, deleted
url | false | string |
description | false | string |
universal_categories | false | string | json hash which follows a particular style "{ parent_id: [cat_a, cat_b] }", e.g.: "{ \"3\": [57, 58] }" stands for selecting categories whose id is 57 or 58, both of them shares a parent category whose id is 3. As for the universal category table, please check out the section "Universal Category"
custom_categories | false | string | json hash. e.g.: "[{ \"prop_id\": 1, \"name\": \"name\", \"value\": \"value\", \"disable\": true }]" stands for selecting the record that matches the given props among uploaded categories. As for how to upload, please check out the section "Custom Categories/Tags"
custom_tags | false | string | json hash.  e.g.: "[{ \"prop_id\": 1, \"name\": \"name\", \"value\": \"value\", \"disable\": true }]" stands for selecting the record that matches the given props among uploaded tags. As for how to upload, please check out the section "Custom Categories/Tags"

# Custom Categories/Tags
## List uploaded category/tag

### HTTP Request
`GET http://HOST/api/custom_props/{TYPE}`

`{TYPE}` could be either "custom_tag" or "custom_category".

### Query Parameters

Parameter | Required | Default | Type | Description
--------- | -------- | ------- | ---- | -----------
keyword | false | None | string | search by keyword
parent_id | false | None | int | query by parent_id
order | false | "id,asc" | string | Order. `<column>,<asc or desc>` eg: "id,desc" supported ordering fields: "name", "parent_id", "value", "disabled", "updated_at", "created_at"
offset | false | 0 | long | Offset
limit | false | 25 | long | Limit

## Upload a New Category/Tag Mapping Table
If you want to use your own categories or tags, please upload the maping to our server first.
Thus you can use them by assigning `custom_categories` or `custom_tags` to placments.
For more detail, check out relevant sections of placment management.

### HTTP Request
`POST http://HOST/api/custom_props/upload/{TYPE}`

`{TYPE}` could be either "tag" or "category"

### Query Parameters

Parameter | Required | Default | Description
--------- | -------- | ------- | -----------
file | true | None | yaml file, please check out the example below

### example yaml file
```
- tag_id: 1
  category: # it could be empty
  value: "1" # the unique value
  name: "酒店" # name displayed on console
  shown: true # visible or not
- tag_id: 2
  category:
  value: "2"
  name: "机票"
  shown: true
- tag_id: 3
  category:
  value: "3"
  name: "火车票"
  shown: true
- tag_id: 11
  category: 1 # it belongs to the record whose id is 1 (酒店)
  value: "11"
  name: "酒店_出发地"
  shown: true
```

# Reports

## Get Recent Reports

> Example Request:

```shell
curl -H "X-Requested-With: XMLHttpRequest" \
     -H "x-access-token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJwbGF0Zm9ybV9pZCI6IjEyIiwidXNlcm5hbWUiOiJzdXBlcmFkbWluIiwidG9rZW4iOiIxMDU1M2ZjZTk0ZjE2YmQ5NGJmNWZjZTZjNzJjYTVkOTQwNjY2N2QwNmI0NWQ4OWE0MTc3OGYwMDFlOTA5MWNiIn0.fMZy0m0J6yaTQabbF9LCQmgdV0ujF1wfthCKmELhiIs" \
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
     -H "x-access-token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJwbGF0Zm9ybV9pZCI6IjEyIiwidXNlcm5hbWUiOiJzdXBlcmFkbWluIiwidG9rZW4iOiIxMDU1M2ZjZTk0ZjE2YmQ5NGJmNWZjZTZjNzJjYTVkOTQwNjY2N2QwNmI0NWQ4OWE0MTc3OGYwMDFlOTA5MWNiIn0.fMZy0m0J6yaTQabbF9LCQmgdV0ujF1wfthCKmELhiIs" \
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

## Detail of a Specific Report Request

> Example Request:

```shell
curl -H "X-Requested-With: XMLHttpRequest" \
     -H "x-access-token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJwbGF0Zm9ybV9pZCI6IjEyIiwidXNlcm5hbWUiOiJzdXBlcmFkbWluIiwidG9rZW4iOiIxMDU1M2ZjZTk0ZjE2YmQ5NGJmNWZjZTZjNzJjYTVkOTQwNjY2N2QwNmI0NWQ4OWE0MTc3OGYwMDFlOTA5MWNiIn0.fMZy0m0J6yaTQabbF9LCQmgdV0ujF1wfthCKmELhiIs" \
    http://HOST/api/report_requests/1
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
`GET http://HOST/api/report_requests/{REPORT_REQUEST_ID}`

## Get the Review of a Specific Report

> Example Request:

```shell
curl -H "X-Requested-With: XMLHttpRequest" \
     -H "x-access-token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJwbGF0Zm9ybV9pZCI6IjEyIiwidXNlcm5hbWUiOiJzdXBlcmFkbWluIiwidG9rZW4iOiIxMDU1M2ZjZTk0ZjE2YmQ5NGJmNWZjZTZjNzJjYTVkOTQwNjY2N2QwNmI0NWQ4OWE0MTc3OGYwMDFlOTA5MWNiIn0.fMZy0m0J6yaTQabbF9LCQmgdV0ujF1wfthCKmELhiIs" \
    http://HOST/api/report_requests/1/review
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
     -H "x-access-token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJwbGF0Zm9ybV9pZCI6IjEyIiwidXNlcm5hbWUiOiJzdXBlcmFkbWluIiwidG9rZW4iOiIxMDU1M2ZjZTk0ZjE2YmQ5NGJmNWZjZTZjNzJjYTVkOTQwNjY2N2QwNmI0NWQ4OWE0MTc3OGYwMDFlOTA5MWNiIn0.fMZy0m0J6yaTQabbF9LCQmgdV0ujF1wfthCKmELhiIs" \
    http://HOST/api/report_requests/1/review?format=xlsx
```

### HTTP Request
`GET http://HOST/api/report_requests/{REPORT_REQUEST_ID}/review`

## Create a New Report

> Example Request:

```shell
curl -H "X-Requested-With: XMLHttpRequest" \
     -H "x-access-token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJwbGF0Zm9ybV9pZCI6IjEyIiwidXNlcm5hbWUiOiJzdXBlcmFkbWluIiwidG9rZW4iOiIxMDU1M2ZjZTk0ZjE2YmQ5NGJmNWZjZTZjNzJjYTVkOTQwNjY2N2QwNmI0NWQ4OWE0MTc3OGYwMDFlOTA5MWNiIn0.fMZy0m0J6yaTQabbF9LCQmgdV0ujF1wfthCKmELhiIs" \
    -X POST \
    --data "report_reqeust[name]=name" \
    http://HOST/api/report_requests
```

> Example Response:

```
HTTP status code 201
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
     -H "x-access-token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJwbGF0Zm9ybV9pZCI6IjEyIiwidXNlcm5hbWUiOiJzdXBlcmFkbWluIiwidG9rZW4iOiIxMDU1M2ZjZTk0ZjE2YmQ5NGJmNWZjZTZjNzJjYTVkOTQwNjY2N2QwNmI0NWQ4OWE0MTc3OGYwMDFlOTA5MWNiIn0.fMZy0m0J6yaTQabbF9LCQmgdV0ujF1wfthCKmELhiIs" \
    -X PUT \
    --data "report_reqeust[name]=name" \
    http://HOST/api/report_requests/1
```

> Example Response:

```
HTTP status code 204
```

### HTTP Request

`PUT http://HOST/api/report_requests/{REPORT_REQUEST_ID}`

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
     -H "x-access-token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJwbGF0Zm9ybV9pZCI6IjEyIiwidXNlcm5hbWUiOiJzdXBlcmFkbWluIiwidG9rZW4iOiIxMDU1M2ZjZTk0ZjE2YmQ5NGJmNWZjZTZjNzJjYTVkOTQwNjY2N2QwNmI0NWQ4OWE0MTc3OGYwMDFlOTA5MWNiIn0.fMZy0m0J6yaTQabbF9LCQmgdV0ujF1wfthCKmELhiIs" \
    -X DELETE \
    http://HOST/api/report_requests/1
```

> Example Response:

```
HTTP status code 204
```

### HTTP Request

`DELETE http://HOST/api/report_requests/{REPORT_REQUEST_ID}`

## Rerun a Specific Report

> Example Request:

```shell
curl -H "X-Requested-With: XMLHttpRequest" \
     -H "x-access-token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJwbGF0Zm9ybV9pZCI6IjEyIiwidXNlcm5hbWUiOiJzdXBlcmFkbWluIiwidG9rZW4iOiIxMDU1M2ZjZTk0ZjE2YmQ5NGJmNWZjZTZjNzJjYTVkOTQwNjY2N2QwNmI0NWQ4OWE0MTc3OGYwMDFlOTA5MWNiIn0.fMZy0m0J6yaTQabbF9LCQmgdV0ujF1wfthCKmELhiIs" \
    -X POST \
    http://HOST/api/report_requests/1/rerun
```

> Example Response:

```
HTTP status code 201
```

### HTTP Request

`POST http://HOST/api/report_requests/{REPORT_REQUEST_ID}/rerun`
