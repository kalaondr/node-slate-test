# Errors

Daytrip uses conventional HTTP response codes to indicate the success or failure of an API request. In general: Codes in the 2xx range indicate success. Codes in the 4xx range indicate an error that failed given the information provided (e.g., a required parameter was omitted, no trip was found for given parameters, etc.). Codes in the 5xx range indicate an error with Daytrip's servers (these are rare).

HTTP Code | Meaning
---------- | -------
400        | Bad Request -- The request could not be understood by the server due to malformed syntax.
401        | Unauthorized -- API key is missing or invalid.
403        | Forbidden -- The requested operation is forbidden.
404        | Not Found -- No trips found, trip option not found, booking not found.
405        | Method Not Allowed -- Invalid HTTP method for given endpoint.
406        | Not Acceptable -- You requested a format that isn't JSON.
500        | Internal Server Error -- We had a problem with our server. Please retry your request.
503        | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.
