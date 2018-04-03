---
title: Exposure API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - php

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Exposure Marketing API! You can use our API help capture data and run promotions such as sweepstakes and contests.

We have language bindings in Shell and PHP! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](https://github.com/lord/slate). Feel free to edit it and use it as a base for your own API's documentation.

# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: Bearer YOUR-TOKEN-HERE"
```

```php
<?php

$headers = [
  'Authorization' => 'Bearer YOUR-TOKEN-HERE',
];
curl_setopt($curl, CURLOPT_HTTPHEADER, $headers);

?>
```

> Make sure to replace `YOUR-TOKEN-HERE` with your API token.

Exposure Marketing uses API tokens to allow access to the API. You can request a new API token at [developer portal](http://example.com/developers).

The API token should be included in all requests in an Authorization header, like this:

`Authorization: Bearer YOUR-TOKEN-HERE`

<aside class="notice">
You must replace <code>YOUR-TOKEN-HERE</code> with your personal API token.
</aside>

# Entries

## Submit an entry

```shell
curl "https://{base_url}/api/v1/promotions/{identifier}/entries" \
  -H "Authorization: Bearer YOUR-TOKEN-HERE" \
  -X POST \
  -d "email=jdoe@example.com&first_name=John&last_name=Doe"
```

```php
<?php

// TODO

?>
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": 1001,
    "entered_at": 1520366874,
    "created_at": 1520366874
  }
}
```

This endpoint creates new entries.

### HTTP Request

`POST https://{base_url}/api/v1/promotions/{identifier}/entries`

### URL Parameters

Parameter | Description
--------- | -----------
`base_url` | Base URL to the API
`identifier` | The identifier of the promotion

### Request Parameters

Parameter | Description
--------- | -----------
`email` | Email address of the registrant. Required if promotion fingerprint type is set to *Email*, otherwise optional. (string, limit: 191 characters)
`fingerprint` | Custom identifier of the registrant. Required if promotion fingerprint type is set to *Custom*, otherwise ignored. (string, limit: 191 characters)
`entered_at` | Custom entry date. Optional. (string, yyyy-mm-dd format)
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
