# Replies

## List

Get a list of replies and their answers.

> GET /api/v01/replies

```shell
curl --location --request GET 'https://webreport.buenno.fi/api/v01/replies' \
--header 'api-auth-token: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' \
-d 'from=2020-12-17T00:00:00+00:00' \
-d 'to=2020-12-19T00:00:00+00:00' \
-d 'limit=1000'
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
      "pf_seller_id": null,
      "pf_product_category": null,
      "pf_target": null,
      "pf_gender": null,
      "pf_age": null,
      "pf_external_id": null,
      "preferred_language": null,
      "question_count": 2,
      "score_sum": 125,
      "avg_score": 62.5,
      "answers": [
        {
          "question": "Lorem ipsum",
          "points": 50,
          "answer": "Sed ut perspiciatis, unde omnis iste natus error sit voluptatem accusantium doloremque laudantium.",
          "question_id": 1234,
          "question_type_id": 1
        },
        {
          "question": "Lorem ipsum 2",
          "points": 75,
          "answer": null,
          "question_id": 1237,
          "question_type_id": 1
        },
        {
          "question": "De finibus bonorum et malorum",
          "points": 0,
          "answer": "qui ratione voluptatem sequi nesciunt, neque porro quisquam est, qui do.",
          "question_id": 2345,
          "question_type_id": 13
        }
      ],
      "updated_at": "2020-12-19T00:00:00Z",
      "created_at": "2020-12-18T00:00:00Z"
    }
  ],
  "total": "2225",
  "limit": "500",
  "offset": "0"
}
```

### URL Parameters

Parameter | Description | Type | Mandatory
--------- | ----------- | ---- | --------
from | Answers from date | Date time ISO 8601  | Yes
to | Answers to date | Date time ISO 8601 | Yes
limit | Max number of answers to return, Default = 500, Max = 1000 | Integer | No
offset | Answer number to start from. Default = 0 | Integer | No
locale | Locale used in question names | string | No

Server is in UTC time. If you want to use local time for api calls use the +00:00 part to provide the offset to UTC.

Each reply contains `question_count`, `score_sum`, and `avg_score`, these 3 belong together:

Name | Meaning
--------- | ----
question_count | The amount of main questions that have points.
score_sum | The sum of all those main questions' points.
avg_score | The average score for this reply; score_sum / question_count.


Each question includes a `question_id` and `question_type_id`. `question_id` is a unique identifier for that question while `question_type_id` indicates which kind of question it is. The possible question types are:

question_type_id | Question type
--------- | ----
1 | Main question
2 | Other question
4 | Admin
5 | Offered product
6 | Shopping goal
7 | Answerer
8 | Age
9 | Gender
10 | Seller's name
11 | Visit date
12 | Visit time
13 | NPS
48 | Product category
49 | Seller's ID
52 | External rating (e.g. imported Google Review)
