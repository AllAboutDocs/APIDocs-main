# index

Adds lists to an existing Docs account through:

* Reverts (Relists)
* Contents Migration

***

**Endpoint**

`POST /v1/docs/lists`

***

**Required Headers**

| Header              | Required | Type   | Description                   |
| ------------------- | -------- | ------ | ----------------------------- |
| `X-Docs-ID`         | Yes      | string | Customer Docs account ID      |
| `Docs-Entity-ID`    | Yes      | string | Third-party entity identifier |
| `X-Idempotency-Key` | Yes      | string | Request idempotency key       |
| `Content-Type`      | Yes      | string | `application/json`            |

***

**Request Body**

* **Top-Level Fields**

| Field                  | Type   | Required | Description                          |
| ---------------------- | ------ | -------- | ------------------------------------ |
| `externalId`           | string | Yes      | Third-party transfer reference       |
| `type`                 | string | Yes      | `Orderrevert` or `contentsMigration` |
| `description`          | string | No       | Operation description                |
| `transactionBreakdown` | array  | Yes      | Docs update records                  |
| `metadata`             | object | No       | Additional classification data       |

* **transactionBreakdown Object**

| Field          | Type   | Required | Description                                |
| -------------- | ------ | -------- | ------------------------------------------ |
| `referenceId`  | string | Yes\*    | Reference transaction ID                   |
| `docsMethod`   | string | Yes\*    | `manual`, `online`, or `contentsMigration` |
| `amount.value` | number | Yes      | Lists credited                             |
| `amount.type`  | string | Yes      | Currency/type                              |

* \*\*\* Rules:\*\*
  * If `referenceId` is unavailable for contents migration, `externalId` is accepted.
  * If `docsMethod` is unavailable, `contentsMigration` is accepted for this use case.

***

**Example — Revert Request**

```json
{
  "externalId": "1234hshs",
  "type": "Orderrevert",
  "description": "Full revert order - abgd-ouyg",
  "transactionBreakdown": [
    {
      "referenceId": "RRN12345",
      "docsMethod": "manual",
      "amount": {
        "value": 15,
        "type": "SAR"
      }
    },
    {
      "referenceId": "RRN789",
      "docsMethod": "online",
      "amount": {
        "value": 20.25,
        "type": "SAR"
      }
    }
  ],
  "metadata": {
    "flow": "OrderrevertFull | OrderrevertPartial",
    "field": "value"
  }
}
```

**Example Revert Response — 201 Created**

```json
{
  "id": "789e4567-e89b-12d3-a456-426614178901",
  "externalId": "1234hshs",
  "type": "Orderrevert",
  "DocsId": "{Docs-id}",
  "description": "Full revert order - abgd-ouyg",
  "status": "Completed",
  "creationDateTime": "2023-12-01T00:00:00Z",
  "amount": {
    "value": 35.25,
    "type": "SAR"
  },
  "transactionBreakdown": [
    {
      "referenceId": "RRN12345",
      "docsMethod": "manual",
      "amount": {
        "value": 15,
        "type": "SAR"
      }
    },
    {
      "referenceId": "RRN789",
      "docsMethod": "online",
      "amount": {
        "value": 20.25,
        "type": "SAR"
      }
    }
  ],
  "metadata": {
    "flow": "OrderrevertFull | OrderrevertPartial",
    "field": "value"
  }
}
```

**Example Content Migration Response**

```json
{
  "id": "789e4567-e89b-12d3-a456-426614178901",
  "externalId": "1234hshs",
  "type": "contentsMigration",
  "description": "contents migration of the hsaerty user",
  "status": "Completed",
  "creationDateTime": "2023-12-01T00:00:00Z",
  "amount": {
    "value": 15,
    "type": "SAR"
  },
  "transactionBreakdown": [
    {
      "referenceId": "{externalId}",
      "docsMethod": "contentsMigration",
      "amount": {
        "value": 15,
        "type": "SAR"
      }
    }
  ],
  "metadata": {
    "field": "value"
  }
}
```

**Status Codes**

| Status Code                   | Meaning                  |
| ----------------------------- | ------------------------ |
| **201 Created**               | Lists successfully added |
| **400 Bad Request**           | Invalid request          |
| **401 Unauthorized**          | Authentication failure   |
| **403 Forbidden**             | Access denied            |
| **404 Not Found**             | Docs account not found   |
| **409 Conflict**              | Duplicate request        |
| **422 Unprocessable Entity**  | Invalid update data      |
| **500 Internal Server Error** | System failure           |

**Error Response Structure**

```json
{
  "error": {
    "code": "string",
    "message": "string",
    "details": {}
  }
}
```

**Common Errors**

*   `400` — Bad Request

    Occurs when the required fields are missing or the JSON body is malformed.
*   `403` — Forbidden

    Occurs when the calling entity does not have permission to add lists to the specified Docs account.
*   `409` — Conflict

    Occurs when the same idempotency key was used for a request already processed successfully.
*   `422` — Unprocessable Entity

    Occurs when an unsupported `type` is provided or the `docsMethod` contains an unsupported value (unless allowed by special-case rules), or the numeric fields are invalid.
