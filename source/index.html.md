---
title: SweepsEngine API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - php

toc_footers:
  - <a href='https://www.sweepsengine.io/register'>Create an Account</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the [SweepsEngine API](https://www.sweepsengine.io)! You can use our API help capture data and run promotions such as sweepstakes and contests.

We have language examples in Shell and PHP! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "..."
  -H "Authorization: Bearer {token}"
```

```php
<?php

$headers = [
  'Authorization' => 'Bearer {token}',
];
curl_setopt($curl, CURLOPT_HTTPHEADER, $headers);
```

> Make sure to replace `{token}` with your API token.

SweepsEngine uses API tokens to allow access to the API. View or request a new API token on your profile's [API Settings](https://www.sweepsengine.io/profile/api) page.

The API token should be included in all requests in an Authorization header, like this:

`Authorization: Bearer {token}`

<aside class="notice">
You must replace <code>{token}</code> with your personal API token.
</aside>

# Promotions

## Show Promotion

```shell
curl "https://api.sweepsengine.io/api/v1/promotions/{identifier}" \
  -H "Authorization: Bearer {token}"
```

```php
<?php

$headers = [
  'Authorization' => 'Bearer {token}',
];

$ch = curl_init();

curl_setopt($ch, CURLOPT_URL, "https://api.sweepsengine.io/api/v1/promotions/{identifier}");
curl_setopt($ch, CURLOPT_HTTPHEADER, $headers);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

$response = curl_exec($ch);

curl_close($ch);
```

> The above command returns JSON structured response like this:

```json
{
  "data": {
    "identifier": "{identifier}",
    "title": "My Awesome Sweeps",
    "starts_at": "2019-02-16T00:00:00-05:00",
    "ends_at": "2019-02-16T00:00:00-05:00",
    "timezone": "America/Detroit",
    "frequency": "Once",
    "fingerprint": "Email",
    "is_open": true
  }
}
```

This enpoint returns details about a promotion.

### HTTP Request

`GET https://api.sweepsengine.io/api/v1/promotions/{identifier}`

### URL Parameters

Parameter | Description
--------- | -----------
`identifier` | The identifier of the promotion

### Request Parameters

(none)

### Response Parameters

Parameter | Description
--------- | -----------
`identifier` | The identifier of the promotion
`title` | Promotion title
`starts_at` | Datetime of promotion start, in ISO 8601 format
`ends_at` | Datetime of promotion end, in ISO 8601 format
`timezone` | Timezone for the promotion
`frequency` | Allowed entry frequency (e.g. Once, Daily, Custom)
`fingerprint` | Fingerprint method (e.g. Email, Custom)
`is_open` | Is promotion currently open and accepting entries?

# Entries

## Create Entry

```shell
curl "https://api.sweepsengine.io/api/v1/promotions/{identifier}/entries" \
  -H "Authorization: Bearer {token}" \
  -X POST \
  -d "email=jdoe@example.com&first_name=John&last_name=Doe"
```

```php
<?php

$headers = [
  'Authorization' => 'Bearer {token}',
];

$data = [
    'first_name' => 'John',
    'last_name' => 'Doe',
    'email' => 'jdoe@example.com',
];

$ch = curl_init();

curl_setopt($ch, CURLOPT_URL, "https://api.sweepsengine.io/api/v1/promotions/{identifier}/entries");
curl_setopt($ch, CURLOPT_POST, 1);
curl_setopt($ch, CURLOPT_HTTPHEADER, $headers);
curl_setopt($ch, CURLOPT_POSTFIELDS, http_build_query($data));
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

$response = curl_exec($ch);

curl_close($ch);
```

> The above command returns JSON structured response like this:

```json
{
  "data": {
    "id": 1001,
    "remote_ip": "192.168.2.10",
    "source": "email campaign",
    "entered_at": "2019-02-28T15:28:44-05:00",
    "created_at": "2019-02-28T15:28:44-05:00"
  }
}
```

This endpoint creates new entries.

### HTTP Request

`POST https://api.sweepsengine.io/api/v1/promotions/{identifier}/entries`

### URL Parameters

Parameter | Description
--------- | -----------
`identifier` | The identifier of the promotion

### Request Parameters

Parameter | Description
--------- | -----------
`email` | Email address of the registrant. Required if promotion fingerprint type is set to *Email*, otherwise optional. (string, limit: 191 characters)
`fingerprint` | Custom identifier of the registrant. Required if promotion fingerprint type is set to *Custom*, otherwise ignored. (string, limit: 191 characters)
`entered_at` | Custom entry date. Optional. (string, allows most common date formats)
`source` | Source of registrant (e.g. newsletter, banner). Optional. (string, limit: 50 characters)
`remote_ip` | IP address of the registrant. Optional. (string, IPv4 or IPv6 format)
`first_name` | First name of the registrant. Optional. (string, limit: 50 characters)
`last_name` | Last name of the registrant. Optional. (string, limit: 50 characters)
`address_1` | Address line 1 of the registrant. Optional. (string, limit: 100 characters)
`address_2` | Address line 2 of the registrant. Optional. (string, limit: 100 characters)
`city` | City of the registrant. Optional. (string, limit: 100 characters)
`state` | State/province of the registrant. Optional. (string, limit: 50 characters)
`postal_code` | Postal code of the registrant. Optional. (string, limit: 10 characters)
`country` | Country of the registrant. Optional. (string, limit: 50 characters)
`phone` | Telephone number of the registrant. Optional. (string, limit: 50 characters)

<aside class="notice">
Custom fingerprints allow you to uniquely identify registrants based on criteria other than email address, such as cell phone number, external user id, or anything else. But with great power comes great responsibility. It is not recommended to allow this value to be supplied directly by the user, and instead determine it server-side, or at least convert all user-supplied values into a common format.
</aside>

### Response Parameters

Parameter | Description
--------- | -----------
`id` | Entry Id
`remote_ip` | Remote IP address of the registrant (if provided during request)
`source` | Source of the entry (if provided during request)
`entered_at` | Datetime of entry, in ISO 8601 format
`created_at` | Datetime of entry creation, in ISO 8601 format