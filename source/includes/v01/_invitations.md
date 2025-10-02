# Invitations

Use following endpoints to invite users to answer question form. Message content to email or SMS is created automatically by Buenno.

## Create invitation

Invite customers to answer to a survey. Use either email or phone to specify how user should receive the invitation. Use prefilled parameters (pf_) to fill required questions for the customer. If prefilled field is missing, the corresponding question will be asked from the customer.

> POST /api/v01/invitations

```shell
curl --location --request POST 'https://webreport.buenno.fi/api/v01/invitations/' \
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
    "pf_product_category": null,
    "pf_target": null,
    "pf_gender": null,
    "pf_age": null,
    "pf_external_id": null,
    "invitation_link": "https://buenno.fi/i/0b6a5ed887f3b89acd08",
    "delivery_method": null,
    "scheduled_at": "2020-12-18T00:00:00+00:00",
    "sent_at": "2020-12-18T00:00:00+00:00",
    "opened_at": "2020-12-19T00:00:00+00:00",
    "answered_at": null,
    "created_at": "2020-12-18T00:00:00+00:00",
    "updated_at": "2020-12-18T00:00:00+00:00"
  }
}
```

> POST /api/v01/invitations

```shell
curl --location --request POST 'https://webreport.buenno.fi/api/v01/invitations/' \
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
    "first_name": null,
    "last_name": null,
    "form_id": 1,
    "pf_timestamp": null,
    "pf_store": null,
    "pf_seller_name": null,
    "pf_product_category": null,
    "pf_target": null,
    "pf_gender": null,
    "pf_age": null,
    "pf_external_id": null,
    "invitation_link": "https://buenno.fi/i/0b6a5ed887f3b89acd08",
    "delivery_method": "delivered_externally",
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

| Parameter           | Description                                                                                                                                            | Type    | Mandatory   |
|---------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|---------|-------------|
| phone               | Phone number to send survey invitation. Phone number should include country code where + is replaced with 00. E.g +358441234567 becomes 00358441234567 | String  | Conditional |
| email               | Email to send survey invitation                                                                                                                        | String  | Conditional |
| deliver_externally  | If true, invitation is not sent by Buenno. An invitation can be created without email or phone                                                         | Boolean | Conditional |
| first_name          | Customer first name                                                                                                                                    | String  | No          |
| last_name           | Customer last name                                                                                                                                     | String  | No          |
| pf_timestamp        | Time of the customer visit, purchase or interaction (seconds since January 1st, 1970).                                                                 | Integer | No          |
| pf_store            | Name of the store where interaction happened                                                                                                           | String  | No          |
| pf_seller_name      | Salesperson name                                                                                                                                       | String  | No          |
| pf_seller_id        | Salesperson ID                                                                                                                                         | String  | No          |
| pf_product_category | Product category                                                                                                                                       | String  | No          |
| pf_target           | Acquisition target                                                                                                                                     | String  | No          |
| pf_gender           | Customer gender                                                                                                                                        | String  | No          |
| pf_age              | Customer age                                                                                                                                           | Integer | No          |
| pf_external_id      | External customer id                                                                                                                                   | String  | No          |
| preferred_language  | Language to use for this invitation, ISO 639‑1 code                                                                                                    | String  | No          |

## List invitations

Lists created invitations.

> GET /api/v01/invitations

```shell
curl --location --request GET 'https://webreport.buenno.fi/api/v01/invitations/' \
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
      "pf_product_category": null,
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
created_after | Invitations created after date | Date time ISO 8601  | No
created_before | Invitations created before date | Date time ISO 8601 | No
limit | Max number of rows to return, Default = 100, Max = 250 | Integer | No
offset | Row number to start from. Default = 0 | Integer | No
form_id | Field to identify form in a case when api-auth-token has access to more than one form. If not filled first active survey form will be used. | Integer | No
