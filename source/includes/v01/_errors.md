# Errors

The Buenno API uses following HTTP status codes on errors.

Code | Possible cause
--------- | ---- 
401 | api-auth-token not found or invalid
403 | Action is not allowed to perform right now.
404 | Given id not found or invalid
404 | Method (GET/PUT/POST/PATCH/DELETE) is not allowed
409 | Created item with a given key already exists

> Example of json error response:

```json
{
  "error_message": "Whoops! Something went wrong."
}
```
