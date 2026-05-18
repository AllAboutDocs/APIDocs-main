# docs create

Creates a new Docs object for a user in the Docs ecosystem.\
If a user doesn't exist, supplying `externalId` automatically creates the user before provisioning the Docs object.

## Endpoint

`POST /v1/docs`

## Required Headers

| Header              | Required | Description                                 |
| ------------------- | -------- | ------------------------------------------- |
| `Docs-Entity-ID`    | Yes      | Unique identifier of the third-party entity |
| `X-Idempotency-Key` | Yes      | Used to safely retry the same request       |
| `Content-Type`      | Yes      | Should be `application/json`                |

## Request Body Schema

```bash
curl -X GET "{BASE_URL}/v1/docs/0f5w7ir5wcqj8ydeih3wpv0807" \
  -H "Docs-Entity-ID: 12345"
```

At least one of owner.id or owner.externalId is required.

| Field              | Type   | Required    | Description                              |
| ------------------ | ------ | ----------- | ---------------------------------------- |
| `type`             | string | Yes         | Type of Docs object to create            |
| `owner.id`         | string | Conditional | Required if `externalId` is not provided |
| `owner.externalId` | string | Conditional | Required if `id` is not provided         |

## Example Request

```json
curl -X POST "{BASE_URL}/v1/docs" \
 -H "Docs-Entity-ID: 12345" \
 -H "X-Idempotency-Key: 9c8c-123abc-99" \
 -H "Content-Type: application/json" \
 -d '{
"type": "full",
"owner": {
"id": "0f5ly1v7p3gqj5ii56e6k6q61x",
"externalId": "unique-customer-code"
}
}'
```

## Example Success Response — 201

```json
{
"id": "asa0a98d0sa8d0sa9d8saasdsa9",
"status": "created",
"owner": {
"id": "0f5ly1v7p3gqj5ii56e6k6q61x",
"externalId": "unique-customer-code"
}
}
```

## Status Codes

| Status Code                  | Meaning                                   |
| ---------------------------- | ----------------------------------------- |
| **201 Created**              | Docs object successfully created          |
| **400 Bad Request**          | Missing or invalid fields                 |
| **401 Unauthorized**         | Authentication failure                    |
| **409 Conflict**             | Duplicate creation due to idempotency key |
| **422 Unprocessable Entity** | Invalid request payload                   |

## Error Response Structure

```json
{
"error": {
"code": "string",
"message": "string",
"details": {}
}
}
```

## Common Errors

*   `400` — Missing Required Fields

    Occurs when type is missing or neither owner.id nor externalId is provided.
*   `409` — Duplicate Request

    Triggered when the same X-Idempotency-Key is reused intentionally or accidentally.
*   `422` — Invalid Data Format

    Occurs when IDs or values do not meet schema requirements.
