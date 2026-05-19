# docs details retrieve by doc id

Retrieves the complete details of a specific Doc using its internal Doc ID.

## Endpoint

`GET /v1/docs/{id}`

## Path Parameters

| Name | Type   | Required | Description                           |
| ---- | ------ | -------- | ------------------------------------- |
| `id` | string | Yes      | Internal unique identifier of the Doc |

## Headers

| Header           | Required | Type   | Description                   |
| ---------------- | -------- | ------ | ----------------------------- |
| `Docs-Entity-ID` | Yes      | string | Third-party entity identifier |

## Example Request

```curl
curl -X GET "{BASE_URL}/v1/docs/0f5w7ir5wcqj8ydeih3wpv0807" \
  -H "Docs-Entity-ID: 12345"
```

## Example Success Response — 200 OK

```json
{
  "id": "0f5w7ir5wcqj8ydeih3wpv0807",
  "status": "Created",
  "owner": {
    "id": "0f5w7ir5wcqj8ydeih3wpv0807",
    "type": "User",
    "externalId": "sample"
  }
}
```

## Status Codes

| Status Code                   | Meaning                    |
| ----------------------------- | -------------------------- |
| **200 OK**                    | Doc successfully retrieved |
| **401 Unauthorized**          | Authentication failed      |
| **403 Forbidden**             | Access denied              |
| **404 Not Found**             | Doc ID not found           |
| **422 Unprocessable Entity**  | Invalid Doc ID             |
| **500 Internal Server Error** | Server failure             |

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

*   `401` — Unauthorized

    Occurs when authentication credentials are missing or invalid.
*   `403` — Forbidden

    Occurs when the calling entity does not have access to the specified Doc.
*   `422` — Unprocessable Entity

    Occurs when the Doc ID does not meet the required schema.
