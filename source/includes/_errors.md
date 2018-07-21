# Errors

<aside class="notice">This error section shows all the errors that are thrown if something went wrong in the request or response body.</aside>

The Ride-My-Way API uses the following error codes:


Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request sucks
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- The requested resourece is for authenticated users only
404 | Not Found -- The specified ride is not found
406 | Not Acceptable -- You have missing/invalid form field(s)
500 | Internal Server Error -- We had a problem with our server. Try again later.