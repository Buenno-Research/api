# Invitations

Use following endpoints to invite users to answer a survey. Message content for email or SMS is created automatically by Buenno.

## Create invitation

Invite customers to answer to a survey. Use either email, phone or deliver_externally to specify how user should receive the invitation. Add required context by filling metadata fields. If suitable field is missing, you can add your own key/value pairs as needed. We do not store empty strings or null values. All metadata values are returned as arrays.

> POST /api/v02/invitations

```shell
curl --location --request POST 'https://webreport.buenno.fi/api/v02/invitations/' \
--header 'api-auth-token: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' \
--header 'Content-Type: application/json' \
--data '{
  "invitation": {
    "phone": "00358441234567",
    "metadata": {
      "first_name": "John",
      "last_name": "Doe",
      "product": ["ProductA", "ProductB"]
    }
  }
}'
```

> Response

```json
{
  "invitation": {
    "id": 1,
    "email": null,
    "phone": "00358441234567",
    "question_form_id": 1,
    "delivery_method": "delivered_by_sms",
    "invitation_link": "https://buenno.fi/i/0b6a5ed887f3b89acd08",
    "metadata": {
      "first_name": ["John"],
      "last_name": ["Doe"],
      "visit_timestamp": null,
      "location": null,
      "employee_name": null,
      "product_category": null,
      "product": ["ProductA", "ProductB"],
      "external_id": null,
      "preferred_language": ["en"]
    },
    "scheduled_at": "2020-12-18T00:00:00+02:00",
    "sent_at": "2020-12-18T00:00:00+02:00",
    "opened_at": "2020-12-19T00:00:00+02:00",
    "answered_at": null,
    "created_at": "2020-12-18T00:00:00+02:00",
    "updated_at": "2020-12-18T00:00:00+02:00"
  }
}
```
### Request Body

| Parameter                             | Description                                                                                                                                            | Type              | Mandatory   |
|---------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------|-------------|
| phone                                 | Phone number to send survey invitation. Phone number should include country code where + is replaced with 00. E.g +358441234567 becomes 00358441234567 | String            | Conditional |
| email                                 | Email to send survey invitation                                                                                                                        | String            | Conditional |
| deliver_externally                    | If true, invitation is not sent by Buenno. An invitation can be created without email or phone                                                         | Boolean           | Conditional |
| metadata                              | Additional customer information (use the fields below when applicable, or add your own key/value pairs as needed)                                      | Object            | No          |
| &nbsp;&nbsp;•&nbsp;first_name         | Customer first name                                                                                                                                    | String / Array | No          |
| &nbsp;&nbsp;•&nbsp;last_name          | Customer last name                                                                                                                                     | String / Array | No          |
| &nbsp;&nbsp;•&nbsp;visit_timestamp    | Time of the customer visit, purchase or interaction (ISO8601: "2025-10-02T06:25:16Z" utc, "2025-10-02T06:25:16+03:00" with timezone)                   | Timestamp / Array | No          |
| &nbsp;&nbsp;•&nbsp;location           | Name of the location where interaction happened                                                                                                        | String / Array | No          |
| &nbsp;&nbsp;•&nbsp;employee_name      | Employee name                                                                                                                                          | String / Array | No          |
| &nbsp;&nbsp;•&nbsp;product_category   | Product category                                                                                                                                       | String / Array | No          |
| &nbsp;&nbsp;•&nbsp;product            | Product                                                                                                                                                | String / Array | No          |
| &nbsp;&nbsp;•&nbsp;external_id        | External customer id                                                                                                                                   | String / Array | No          |
| &nbsp;&nbsp;•&nbsp;preferred_language | Language to use for this invitation, ISO 639‑1 code                                                                                                    | String / Array | No          |



> POST /api/v02/invitations

```shell
curl --location --request POST 'https://webreport.buenno.fi/api/v02/invitations/' \
--header 'api-auth-token: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' \
--header 'Content-Type: application/json' \
--data '{
  "invitation": {
    "deliver_externally": true
  }
}'
```

> Response

```json
{
  "invitation": {
    "id": 1,
    "email": null,
    "phone": null,
    "question_form_id": 1,
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
      "preferred_language": ["en"]
    },
    "scheduled_at": "2020-12-18T00:00:00+02:00",
    "sent_at": "2020-12-18T00:00:00+02:00",
    "opened_at": "2020-12-19T00:00:00+02:00",
    "answered_at": null,
    "created_at": "2020-12-18T00:00:00+02:00",
    "updated_at": "2020-12-18T00:00:00+02:00"
  }
}
```

### Exceptions

Returns `409` if invitation with the given identifier exists, or if the identifier is nonverifiable.

Returns `422` if validation fails (e.g. email or phone invalid, or metadata field value is invalid).

Returns `403` if no active question_form is present.

Returns `404` if question_form_id is invalid.


### Response Fields

Both Create and List endpoints return invitation objects with the same shape.

| Field            | Description                                                                                                                                         | Type               |
|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|--------------------|
| id               | Unique invitation id                                                                                                                                | Integer            |
| email            | Recipient email if email delivery was requested                                                                                                     | String / null      |
| phone            | Recipient phone if SMS delivery was requested                                                                                                       | String / null      |
| question_form_id | Id of the survey this invitation belongs to                                                                                                         | Integer            |
| delivery_method  | Channel used. One of `delivered_by_sms`, `delivered_by_email`, `delivered_externally`. Null on freshly created SMS/email invitations until the sent | String / null      |
| invitation_link  | Unique URL the recipient opens to answer the survey.                                                                                                | String             |
| metadata         | Customer metadata (see Metadata above). All values are returned as arrays.                                                                          | Object             |
| scheduled_at     | When the invitation is scheduled for sending.                                                                                                       | Timestamp / null   |
| sent_at          | When the invitation is actually sent.                                                                                                               | Timestamp / null   |
| opened_at        | When the recipient first opened the invitation link.                                                                                                | Timestamp / null   |
| answered_at      | When the recipient submitted the reply.                                                                                                             | Timestamp / null   |
| created_at       | When the invitation was created.                                                                                                                    | Timestamp          |
| updated_at       | Last modification time.                                                                                                                             | Timestamp          |

All timestamps are ISO 8601 formatted in the server's local timezone (Europe/Helsinki, `+02:00` in winter / `+03:00` during DST).


### Metadata

The `metadata` object accepts any keys you choose. Currently supported value types are `string`, `integer`, `numeric`, `timestamp`, and `boolean`.

When a new key is sent for the first time, the system infers its data type from the value and stores it. After that, the same key can no longer accept values of a different type.

A handful of common keys are pre-created (see the Request Body table above). All of them are of type `string`, except `visit_timestamp`, which is a `timestamp`.

Each value can be submitted as a single value or as an array of values of the same type. All values are returned as arrays.

> Metadata example

```json

"metadata": {
  "location": "Helsinki",
  "product": ["ProductA", "ProductB"],
  "order_total": 4999,
  "visit_timestamp": "2025-10-02T06:25:16Z",
  "is_returning_customer": true
}

```

Note that filtering on the reports is currently supported by the following predefined metadata keys:

- `visit_timestamp`
- `location`
- `employee_name`
- `product_category`
- `product`
- `external_id`

## List invitations

Lists created invitations.

> GET /api/v02/invitations

```shell
curl --location --request GET 'https://webreport.buenno.fi/api/v02/invitations/?from=2020-12-17T00:00:00%2B02:00&to=2020-12-19T00:00:00%2B02:00&limit=100' \
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
      "delivery_method": "delivered_by_sms",
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
        "preferred_language": ["en"]
      },
      "scheduled_at": "2020-12-18T00:00:00+02:00",
      "sent_at": "2020-12-18T00:00:00+02:00",
      "opened_at": "2020-12-19T00:00:00+02:00",
      "answered_at": null,
      "created_at": "2020-12-18T00:00:00+02:00",
      "updated_at": "2020-12-18T00:00:00+02:00"
    }
  ],
  "total": "1",
  "limit": "100",
  "offset": "0"
}
```

### URL Parameters

| Parameter        | Description                                                                                                                                     | Type               | Mandatory |
|------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|--------------------|-----------|
| from             | Return invitations created after this timestamp (exclusive)                                                                                     | Date time ISO 8601 | No        |
| to               | Return invitations created before this timestamp (exclusive)                                                                                    | Date time ISO 8601 | No        |
| limit            | Max number of rows to return, Default = 100, Max = 1000                                                                                         | Integer            | No        |
| offset           | Row number to start from. Default = 0                                                                                                           | Integer            | No        |
| question_form_id | Field to identify question form in a case when api-auth-token has access to more than one form. If not filled first active survey will be used. | Integer            | No        |


