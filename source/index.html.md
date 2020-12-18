---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='mailto:info@buenno.fi'>Contact us for a API Key</a>

includes:
  - errors

search: true

code_clipboard: true

---

# Buenno API Reference

The Buenno API s organized around REST. Our API has predictable resource-oriented URLs, accepts form-encoded request bodies, returns JSON-encoded responses, and uses standard HTTP response codes, authentication, and verbs.

# Authentication

The Buenno API uses API keys to authenticate requests. To send any request to our api, include `api-auth-token to the request header.

Your API keys carry many privileges, so be sure to keep them secure! Do not share your secret API keys in publicly accessible areas such as GitHub, client-side code, and so forth.

<a href='mailto:info@buenno.fi'>Contact us for a API Key</a>

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
    "company_id": 1,
    "company_name": "Example Company Ltd",
    "contact_person": "John Doe"
  }
}
```

# Errors

The Buenno API uses following status codes on errors.

Code | Possible cause
--------- | ---- 
401 | api-auth-token not found or invalid
403 | Action is not allowed to perform right now.
404 | If the given id not found or invalid
405 | Method (GET/PUT/POST/PATCH/DELETE) is not allowed
409 | Created item with a given key already exists

> Example of json error response:

```json
{
  "error_message": "Sorry, method not allowed."
}
```

# Survey

Survey definition here so that developer understands it. Survey questions and settings are by Buenno staff.

## List surveys

Get a list of surveys.

### URL Parameters (optional)

Parameter | Type | Description
--------- | ---- | -----------
active (optional) | Boolean | Filter by ongoing surveys
starting_after (optional) | Timestamp | 
ending_before (optional) | Timestamp |
limit (optional) | Integer | Limit results
offset (optional) | Integer | Offset results

> GET /api/v01/surveys

```shell
curl --location --request GET 'https://buenno-research.io/api/v01/surveys' \
--header 'api-auth-token: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' \
-d 'active=true' \
-d 'starting_after=1234567890' \
-d 'ending_before=1234567890' \
-d 'limit=100' \
-d 'offset=0'
```

> Response

```json
{
  "surveys": [
    {
      "id": 1,
      "name": "Survey name",
      "active": true,
      "updated_at": "2020-12-19T00:00:00+00:00",
      "created_at": "2020-12-18T00:00:00+00:00"
    }
  ]
}
```

# Invitations

Use following endpoints to invite users to answer survey questions via email or SMS. Message content to email or SMS is created automatically by Buenno.

## Create invitation

Invite user to answer to a survey. Returns `409` if invitation with given identifier exists.

Returns `403` if survey is not active.

### URL Parameters

Parameter | Description
--------- | -----------
:id | Active survey id
invitation_id | Phone number or email

> POST /api/v01/surveys/:id/invite

```shell
curl --location --request POST '/api/v01/surveys/:id/invite' \
--header 'api-auth-token: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' \
-d 'invitation_id=firstname.lastname@example.com'
```

> Response

```json
{
  "invitation": {
    "id": 1,
    "survey_id": 1,
    "invitation_id": "+358441234567",
    "updated_at": "2020-12-18T00:00:00+00:00",
    "created_at": "2020-12-18T00:00:00+00:00"
  }
}
```

## List invitations

Lists created invitations.

# Replies

## List

Get a list of replies and their results. Individual answers

> GET /api/v01/surveys/:id/replies

```shell
curl --location --request GET '/api/v01/surveys/1/replies' \
--header 'api-auth-key: 4704c2a7-3646-42ce-9cf1-15e1935d49d3' \
-d 'starting_after=' \
-d 'ending_before=' \
-d 'limit=100'
```

> Response

```json
{
  "replies": [
    {
      "id": 1,
      "name": "Survey name",
      "invite_id": "+358441234567",
      "user_email": "",
      "user_phone": "+358441234567",
      "updated_at": "2020-12-19T00:00:00+00:00",
      "created_at": "2020-12-18T00:00:00+00:00"
    }
  ]
}
```

# Answers

Get individual reply answers.

# Reports

Get survey reports.
