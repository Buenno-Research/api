# Authentication

The Buenno API uses API keys to authenticate requests. To send any request to our api, include `api-auth-token` to the request header.

Your API keys carry many privileges, so be sure to keep them secure! Do not share your secret API keys in publicly accessible areas such as GitHub, client-side code, and so forth.

<a href='mailto:info@buenno.fi'>Contact us for an API Key</a>

## Get token info

Test that your api-auth-token is valid. Token info includes information of accessible forms.

> GET /api/v01/token-info

```shell
# Include your api-auth-token to each request
curl --location --request GET 'https://webreport.buenno.fi/api/v01/token-info' \
--header 'api-auth-token: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'
```

> Response:

```json
{
  "api_token": 
  {
    "name": "Example CRM token",
    "forms": [
      {
        "id": 1,
        "name": "Example Form 2021",
        "company_name": "Example Company Ltd"
      }
    ]
  }
}
```
