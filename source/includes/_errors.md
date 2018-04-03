# Errors

```json
{
  "error": {
    "code": "NOT-AUTHENTICATED",
    "message": "User could not be authenticated."
  }
}
```

All errors return a non-2xx HTTP status response, and an error object with the following parameters:

Parameter | Description
--------- | -----------
`code` | Unique identifier for the error state encountered.
`message` | More detail about the error. For some errors (e.g. validation failure), message may vary to include more information.

<aside class="notice">
For handling errors we recommend inspecting the value of <code>code</code>, as http status codes may be used for multiple errors, and the detail provided by `message` is subject to change.
</aside>

Here is a full listing of codes, HTTP statuses, and their meaning.

Error Code | HTTP Status | Meaning
---------- | ----------- | -------
`MAX-ENTRIES` | 422 | Registrant has recevied max entries for this promotion or period.
`NOT-AUTHENTICATED` | 401 | User could not be authenticated. Usually the API token is unknown/missing.
`NOT-FOUND` | 404 | Resource not found, or user does not have access to it.
`NOT-OPEN` | 404 | Promotion is not open or currently accepting entries.
`VALIDATION-FAILED` | 400 | There were one or more validation failures for the request. <code>message</code> will contain more detail about the first error encountered.

