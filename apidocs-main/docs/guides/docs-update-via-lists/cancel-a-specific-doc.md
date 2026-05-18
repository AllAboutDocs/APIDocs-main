# cancel a specific doc

This request cancels a specific docs transfer that is initiated by the user. For example, the user may request the cancellation of a revert to Docs transaction and initiate the request for revert to source. The cancellation request contains the following:

**Query parameters - Required\***

* `id` - the unique identifier created internally by Docs for each successful docs transfer
* `X-Docs-ID` - the unique customer Docs account ID
* `Docs-Entity-ID` - the unique identifier of the third party entity

**URL**

`{URL}/v1/docs/lists/{id}/cancel`

**Method**

PATCH

**SUCCESS RESPONSE**

200: The requested docs is canceled.

**SAMPLE RESPONSE**

```json
{
  "id": "0f5w7ir5wcqj8ydeih3wpv0807",
  "externalId": "1234hshs",
  "DocsId": "{Docs-id}",
  "type": "Orderrevert",
  "status": "Completed",
  "description": "string",
  "creationDateTime": "2023-12-01T00:00:00Z",
  "amount": {
    "type": "SAR",
    "value": 5
  },
  "transactionBreakdown": [
    {
      "referenceId": "RRN12345 ",
      "docsMethod": "manual | online",
      "amount": {
        "type": "SAR",
        "value": 5
      }
    }
  ],
  "metadata": {
    "flow": "OrderrevertFull | OrderrevertPartial"
  }
}
```
