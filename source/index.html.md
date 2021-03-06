---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='mailto:info@buenno.fi'>Contact us for an API Key</a>

search: true

code_clipboard: true

---

# Buenno API Reference

The Buenno API s organized around REST. Our API has predictable resource-oriented URLs, accepts form-encoded request bodies, returns JSON-encoded responses, and uses standard HTTP response codes, authentication, and verbs.

# Authentication

The Buenno API uses API keys to authenticate requests. To send any request to our api, include `api-auth-token to the request header.

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

# Invitations

Use following endpoints to invite users to answer question form. Message content to email or SMS is created automatically by Buenno.

## Create invitation

Invite customers to answer to a survey. Use either email or phone to specify how user should receive the invitation. Use prefilled parameters (pf_) to fill required questions for the customer. If prefilled field is missing, the corresponding question will be asked from the customer.

> POST /api/v01/invitations

```shell
curl --location --request POST '/api/v01/invitations/' \
--header 'api-auth-token: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' \
-d 'phone=00358441234567'
```

> Response

```json
{
  "invitation": {
    "id": 1,
    "email": null,
    "phone": "00358441234567",
    "first_name": null,
    "last_name": null,
    "form_id": 1,
    "pf_timestamp": null,
    "pf_store": null,
    "pf_seller_name": null,
    "pf_target": null,
    "pf_gender": null,
    "pf_age": null,
    "pf_external_id": null,
    "invitation_link": "https://buenno.fi/i/0b6a5ed887f3b89acd08",
    "scheduled_at": "2020-12-18T00:00:00+00:00",
    "sent_at": "2020-12-18T00:00:00+00:00",
    "opened_at": "2020-12-19T00:00:00+00:00",
    "answered_at": null,
    "created_at": "2020-12-18T00:00:00+00:00",
    "updated_at": "2020-12-18T00:00:00+00:00"
  }
}
```

### Exceptions

Returns `409` if invitation with given identifier exists.

Returns `403` if no active form is present.

Returns `404` if form_id is invalid.

### URL Parameters

Parameter | Description | Type | Mandatory
--------- | ----------- | ---- | --------
phone | Phone number to send survey invitation. Phone or Email is mandatory. Phone number should include country code where + is replaced with 00. E.g +358441234567 becomes 00358441234567 | String | -
email | Email to send survey invitation. Phone or Email is mandatory. | String | -
first_name | Customer first name | String | No
last_name | Customer last name | String | No
pf_timestamp | Time of the customer visit, purchase or interaction (in seconds). | Integer | No
pf_store | Name of the store where interaction happened | String | No
pf_seller_name | Salesperson name | String | No
pf_target | Acquisition target | String | No
pf_gender | Customer gender | String | No
pf_age | Customer age | Integer | No
pf_external_id | External user id | String | No

## List invitations

Lists created invitations.

> GET /api/v01/invitations

```shell
curl --location --request GET '/api/v01/invitations/' \
--header 'api-auth-token: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'
```

> Response

```json
{
  "invitations": [
    {
      "id": 1,
      "email": null,
      "phone": "00358441234567",
      "first_name": null,
      "last_name": null,
      "form_id": 1,
      "pf_timestamp": null,
      "pf_store": null,
      "pf_seller_name": null,
      "pf_target": null,
      "pf_gender": null,
      "pf_age": null,
      "pf_external_id": null,
      "scheduled_at": "2020-12-18T00:00:00+00:00",
      "sent_at": "2020-12-18T00:00:00+00:00",
      "opened_at": "2020-12-19T00:00:00+00:00",
      "answered_at": null,
      "created_at": "2020-12-18T00:00:00+00:00",
      "updated_at": "2020-12-18T00:00:00+00:00"
    }
  ]
}
```

### URL Parameters

Parameter | Description | Type | Mandatory
--------- | ----------- | ---- | --------
form_id | Field to identify form in a case when api-auth-token has access to more than one form. If not filled first active survey form will be used. | Integer | No

# Replies

## List

Get a list of replies and their answers. 

> GET /api/v01/replies

```shell
curl --location --request GET '/api/v01/replies' \
--header 'api-auth-token: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' \
-d 'created_after=2020-12-17T00:00:00+00:00' \
-d 'created_before=2020-12-19T00:00:00+00:00' \
-d 'limit=100'
```

> Response

```json
{
  "replies": [
    {
      "id": 1,
      "name": "Example Survey 12/2020",
      "email": "",
      "phone": "00358441234567",
      "first_name": null,
      "last_name": null,
      "pf_timestamp": null,
      "pf_store": null,
      "pf_seller_name": null,
      "pf_target": null,
      "pf_gender": null,
      "pf_age": null,
      "pf_external_id": null,
      "answers": [
        {
          "question": "Lorem ipsum",
          "points": 50,
          "answer": "Sed ut perspiciatis, unde omnis iste natus error sit voluptatem accusantium doloremque laudantium."
        },
        {
          "question": "De finibus bonorum et malorum",
          "points": 0,
          "answer": "qui ratione voluptatem sequi nesciunt, neque porro quisquam est, qui do."
        }
      ],
      "updated_at": "2020-12-19T00:00:00Z",
      "created_at": "2020-12-18T00:00:00Z"
    }
  ]
}
```

### URL Parameters

Parameter | Description | Type | Mandatory
--------- | ----------- | ---- | --------
created_after | Answers after date | Date time ISO 8601  | No
created_before | Answers before date | Date time ISO 8601 | No
limit | Max number of rows to return, Default = 100 | Integer | No
offset | Row number to start from. Default = 0 | Integer | No
