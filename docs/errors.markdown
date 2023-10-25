Accounts API uses conventional HTTP response codes to indicate the success or failure of an API request.

## Return Codes

Code    | Description
------  | ---
**2XX** | The API call was successful.
**4XX** | The API call had an error. The error will be encoded in the body of the response.
**5XX** | The API call was unsuccessful. You should retry later.

##### Specific return codes

Code     | Description
-------- | ---
`200 OK` | The request was successful.
`201 Created`      | The request was successful and a resource is created.
`400 Bad Request`  | The request could not be understood or required parameters were missing.
`401 Unauthorized` | Authentication failed or user doesn't have permissions for requested operation.
`403 Forbidden`    | Access denied, the operation is not allowed.
`404 Not Found`    | Resource was not found.
`405 Method Not Allowed`    | Requested method is not supported for resource.
`409 Conflict`     | Request could not be completed due to conflicting information.
`412 Precondition failed `  | Request could not be completed due to one of the preconditions is not accomplished.
`500 Internal server error` | Internal server error. Try again later.
`503 Service Unavailable`   | Service is temporarily unavailable. Try again later.

## Schema returned when errors
When there is a 4XX error, the errors array will be informed to help debug errors.

Error response schema :
```
  {
    "error_response": {
      "properties": {
        "errors": [
          {
            "type": {
              "description": "Error Type",
              "required": true,
              "type": "string",
              "enum": [
                "json",
                "form",
                "header",
                "query"
              ]
            },
            "datapath": {
              "description": "Natural path to the error message",
              "required": false,
              "type": "string",
              "example": "email"
            },
            "keyword": {
              "description": "Keyword that failed validation",
              "required": false,
              "type": "string",
              "example": "format"
            },
            "schema": {
              "description": "The schema value that failed validation",
              "required": false,
              "type": "any",
              "example": true
            },
            "data": {
              "description": "The data that failed validation",
              "required": false,
              "type": "any",
              "example": "Pasw@rd"
            },
            "message": {
              "description": "Message Description",
              "required": true,
              "type": "string",
              "example": "Missing required property: email"
            }
          }
          ],
        "stack": {
          "description": "Stack trace of the error",
          "required": false,
          "type": "string",
          "example": "BadRequestError: Request failed to validate against RAML definition\\n    at createValidationError"
        }
      }
    }
  }
```