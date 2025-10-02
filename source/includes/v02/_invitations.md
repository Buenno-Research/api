# Invitations

Use following endpoints to invite users to answer question form. Message content to email or SMS is created automatically by Buenno.

## Create invitation

Invite customers to answer to a survey. Use either email or phone to specify how user should receive the invitation. Use prefilled parameters (pf_) to fill required questions for the customer. If prefilled field is missing, the corresponding question will be asked from the customer.

> POST /api/v02/invitations

```shell
curl --location --request POST 'https://webreport.buenno.fi/api/v02/invitations/' \
--header 'api-auth-token: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' \
-d 'phone=00358441234567' \
-d 'metadata[first_name]=John' \
-d 'metadata[last_name]=Doe' \
-d 'metadata[product][]=ProductA' \
-d 'metadata[product][]=ProductB'
```

> Response

```json
{
  "invitation": {
    "id": 1,
    "email": null,
    "phone": "00358441234567",
    "delivery_method": null,
    "invitation_link": "https://buenno.fi/i/0b6a5ed887f3b89acd08",
    "metadata": {
      "first_name": null,
      "last_name": null,
      "visit_timestamp": null,
      "location": null,
      "employee_name": null,
      "product_category": null,
      "product": null,
      "external_id": null,
      "preferred_language": "en"
    },
    "scheduled_at": "2020-12-18T00:00:00+00:00",
    "sent_at": "2020-12-18T00:00:00+00:00",
    "opened_at": "2020-12-19T00:00:00+00:00",
    "answered_at": null,
    "created_at": "2020-12-18T00:00:00+00:00",
    "updated_at": "2020-12-18T00:00:00+00:00"
  }
}
```

> POST /api/v02/invitations

```shell
curl --location --request POST 'https://webreport.buenno.fi/api/v02/invitations/' \
--header 'api-auth-token: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' \
-d 'deliver_externally=true'
```

> Response

```json
{
  "invitation": {
    "id": 1,
    "email": null,
    "phone": "00358441234567",
    "delivery_method": "delivered_externally",
    "invitation_link": "https://buenno.fi/i/0b6a5ed887f3b89acd08",
    "metadata": {
      "first_name": null,
      "last_name": null,
      "visit_timestamp": null,
      "location": null,
      "employee_name": null,
      "product_category": null,
      "product": null,
      "external_id": null,
      "preferred_language ": "en"
    },
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

| Parameter                             | Description                                                                                                                                            | Type            | Mandatory   |
|---------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|-------------|
| phone                                 | Phone number to send survey invitation. Phone number should include country code where + is replaced with 00. E.g +358441234567 becomes 00358441234567 | String          | Conditional |
| email                                 | Email to send survey invitation                                                                                                                        | String          | Conditional |
| deliver_externally                    | If true, invitation is not sent by Buenno. An invitation can be created without email or phone                                                         | Boolean         | Conditional |
| metadata                              | Additional customer information (use the fields below when applicable, or add your own key/value pairs as needed)                                      | Object          | No          |
| &nbsp;&nbsp;•&nbsp;first_name         | Customer first name                                                                                                                                    | String          | No          |
| &nbsp;&nbsp;•&nbsp;last_name          | Customer last name                                                                                                                                     | String          | No          |
| &nbsp;&nbsp;•&nbsp;visit_timestamp    | Time of the customer visit, purchase or interaction (ISO8601: "2025-10-02T06:25:16Z" utc, "2025-10-02T06:25:16+03:00" with timezone)                   | Integer         | No          |
| &nbsp;&nbsp;•&nbsp;location           | Name of the location where interaction happened                                                                                                        | String          | No          |
| &nbsp;&nbsp;•&nbsp;employee_name      | Employee name or names                                                                                                                                 | String or Array | No          |
| &nbsp;&nbsp;•&nbsp;product_category   | Product category or categories                                                                                                                         | String or Array          | No          |
| &nbsp;&nbsp;•&nbsp;product            | Product or products                                                                                                                                    | String or Array          | No          |
| &nbsp;&nbsp;•&nbsp;external_id        | External customer id                                                                                                                                   | String          | No          |
| &nbsp;&nbsp;•&nbsp;preferred_language | Language to use for this invitation, ISO 639‑1 code                                                                                                    | String          | No          |

## List invitations

Lists created invitations.

> GET /api/v02/invitations

```shell
curl --location --request GET 'https://webreport.buenno.fi/api/v02/invitations/' \
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
      "question_form_id": 1,
      "metadata": {
        "first_name": null,
        "last_name": null,
        "visit_timestamp": null,
        "location": null,
        "employee_name": null,
        "product_category": null,
        "product": null,
        "external_id": null,
        "preferred_language ": "en"
      },
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

Parameter | Description                                                                                                                                     | Type | Mandatory
--------- |-------------------------------------------------------------------------------------------------------------------------------------------------| ---- | --------
from | Invitations created after date                                                                                                                  | Date time ISO 8601  | No
to | Invitations created before date                                                                                                                 | Date time ISO 8601 | No
limit | Max number of rows to return, Default = 100, Max = 250                                                                                          | Integer | No
offset | Row number to start from. Default = 0                                                                                                           | Integer | No
question_form_id | Field to identify question form in a case when api-auth-token has access to more than one form. If not filled first active survey will be used. | Integer | No
