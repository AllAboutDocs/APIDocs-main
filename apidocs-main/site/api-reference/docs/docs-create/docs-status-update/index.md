# index

Updates the status of an existing Doc using its internal Doc ID. The request uses JSON Patch format.

***

**Endpoint**

```
PATCH /v1/docs/{id}
```

***

**Path Parameters**

| Name | Type   | Required | Description                           |
| ---- | ------ | -------- | ------------------------------------- |
| `id` | string | Yes      | Internal unique identifier of the Doc |

***

**Headers**

| Header           | Required | Type   | Description                   |
| ---------------- | -------- | ------ | ----------------------------- |
| `Docs-Entity-ID` | Yes      | string | Third-party entity identifier |
| `Content-Type`   | Yes      | string | `application/json`            |

***

**Request Body (JSON Patch)**

| Field   | Type   | Required | Description                               |
| ------- | ------ | -------- | ----------------------------------------- |
| `path`  | string | Yes      | Property to update (`/status`)            |
| `op`    | string | Yes      | Operation to perform (`replace`)          |
| `value` | string | Yes      | New status (`active`, `pending`, `block`) |

***

**Example Request**

```bash
curl -X PATCH "{BASE_URL}/v1/docs/0f5w7ir5wcqj8ydeih3wpv0807" \  -H "Docs-Entity-ID: 12345" \  -H "Content-Type: application/json" \  -d '[  {  "path": "/status",  "op": "replace",  "value": "block"  }  ]'
```

**Example Success Response — 200 OK**

```json
{  "id": "0f5w7ir5wcqj8ydeih3wpv0807",  "status": "Created",  "owner": {  "id": "0f5w7ir5wcqj8ydeih3wpv0807",  "type": "User",  "externalId": "sample"  } }
```

**Status Codes**

| Status Code                   | Meaning                         |
| ----------------------------- | ------------------------------- |
| **200 OK**                    | Doc status successfully updated |
| **400 Bad Request**           | Invalid patch format            |
| **401 Unauthorized**          | Authentication failed           |
| **403 Forbidden**             | Access denied                   |
| **404 Not Found**             | Doc ID not found                |
| **422 Unprocessable Entity**  | Invalid status value            |
| **500 Internal Server Error** | Server failure                  |

**Error Response Structure**

```json
{  "error": {  "code": "string",  "message": "string",  "details": {}  } }
```

**Common Errors**

*   `400` — Bad Request

    Occurs when the Patch operation is malformed, or an invalid path, op, or value is provided.
*   `403` — Forbidden

    Occurs when the calling entity does not have permission to update the Doc.
*   `404` — Not Found

    Occurs when the specified Doc ID does not exist
