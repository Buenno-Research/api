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
curl --location --request GET 'https://buenno-research.io/api/v01/token-info' \
--header 'api-auth-token: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'
```

> Response:

```json
{
  "token-info": 
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
405 | Method (GET/PUT/POST/PATCH/DELETE) is not allowed
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

Invite customers to answer to a survey. Use prefilled parameters (pf_) to fill required questions for the customer. If prefilled field is missing, the corresponding question will be asked from the customer.

> POST /api/v01/invitations

```shell
curl --location --request POST '/api/v01/invitations/' \
--header 'api-auth-token: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' \
-d 'invitation_id=firstname.lastname@example.com'
```

> Response

```json
{
  "invitation": {
    "id": 1,
    "form_id": 1,
    "email": null,
    "phone": "00358441234567",
    "delay": 0,
    "retries": 1,
    "pf_timestamp": null,
    "pf_store": null,
    "pf_seller_name": null,
    "pf_target": null,
    "pf_first_name": null,
    "pf_last_name": null,
    "pf_gender": null,
    "pf_age": null,
    "sent_at": "2020-12-18T00:00:00+00:00",
    "answered_at": null,
    "updated_at": "2020-12-18T00:00:00+00:00",
    "created_at": "2020-12-18T00:00:00+00:00"
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
form_id | Field to identify form in a case when api-auth-token has access to more than one form. If not filled first active survey form will be used. | Integer | No
delay | Number of seconds to delay the invitation to the customer, default = 0 | Integer | No
retries | Number of retries, default = 1 | Integer | No
pf_timestamp | Time of the customer visit, purchase or interaction. | Integer | No
pf_store | Name of the store where interaction happened | String | No
pf_seller_name | Salesperson name | String | No
pf_target | Acquisition target | String | No
pf_name | Customer name | String | No
pf_gender | Customer gender | String | No
pf_age | Customer age | Integer | No

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
      "form_id": 1,
      "invitation_id": "+358441234567",
      "delay": 0,
      "retries": 1,
      "pf_timestamp": null,
      "pf_store": null,
      "pf_seller_name": null,
      "pf_target": null,
      "pf_name": null,
      "pf_gender": null,
      "pf_age": null,
      "sent_at": "2020-12-18T00:00:00+00:00",
      "answered_at": null,
      "updated_at": "2020-12-18T00:00:00+00:00",
      "created_at": "2020-12-18T00:00:00+00:00"
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
-d 'created_after=2020-12-18T00:00:00+00:00' \
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
      "invite_id": "+358441234567",
      "user_email": "",
      "user_phone": "+358441234567",
      "answers": [
        ...
      ],
      "updated_at": "2020-12-19T00:00:00+00:00",
      "created_at": "2020-12-18T00:00:00+00:00"
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
