# docs contents list by doc id

Retrieves the current contents and expiring contents associated with a specific Doc using its internal Doc ID. I am testing the change request workflow.

## Endpoint

`GET /v1/docs/{id}/contents`

## Path Parameters

| Name | Type   | Required | Description                           |
| ---- | ------ | -------- | ------------------------------------- |
| `id` | string | Yes      | Internal unique identifier of the Doc |

## Headers

| Header           | Required | Type   | Description                   |
| ---------------- | -------- | ------ | ----------------------------- |
| `Docs-Entity-ID` | Yes      | string | Third-party entity identifier |

## Example Request

```bash
curl -X GET "{BASE_URL}/v1/docs/0f5w7ir5wcqj8ydeih3wpv0807/contents" \
  -H "Docs-Entity-ID: 12345"
```

## Example Success Response — 200 OK

```json
{
  "id": "0f5w7ir5wcqj8ydeih3wpv0807",
  "aggregatedcontents": {
    "primary": {
      "type": "SAR",
      "value": 5
    }
  },
  "accounts": [
    {
      "accountType": "string",
      "contents": {
        "type": "SAR",
        "value": 5
      },
      "expiringcontents": [
        {
          "amount": {
            "type": "SAR",
            "value": 5
          },
          "expirationDateTime": "2023-12-12T10:16:38Z"
        }
      ]
    }
  ]
}
```

## Status Codes

| Status Code                  | Meaning                         |
| ---------------------------- | ------------------------------- |
| **200 OK**                   | Contents successfully retrieved |
| **401 Unauthorized**         | Authentication failed           |
| **403 Forbidden**            | Access denied                   |
| **404 Not Found**            | Doc ID not found                |
| **422 Unprocessable Entity** | Invalid Doc ID                  |

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

* `400` — Bad Request\
  Occurs when the Doc ID format is invalid or required path parameters are missing
* `422` — Unprocessable Entity\
  Occurs when the Doc ID does not match the expected schema
