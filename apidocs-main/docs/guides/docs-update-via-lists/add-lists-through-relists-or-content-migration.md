# add lists through relists or content migration

This request adds lists to an existing customer Docs account via relists or contents migrations. This endpoint credits lists to a customer's Docs account as part of:

* A **relist/revert operation**, or
* A **contents migration operation**

Each request records:

* The update source (manual or online)
* The amount credited
* A reference ID for reconciliation and reporting

## When to Use This Endpoint

Use this API when you need to:

* Credit lists after an **order revert**
* Migrate contents from another system into Docs
* Adjust customer balances due to operational corrections
* Track Docs updates for reconciliation and reporting

## Prerequisites

Ensure you have the following before making a request:

### Query Parameters - Required\*

* `X-Docs-ID` - the unique customer Docs account ID
* `Docs-Entity-ID` - the unique identifier of the third party entity
* `X-Idempotency-Key` - the unique server-created key to confirm subsequent retries of the same request

### Request Parameters - Required\*

* `externalId` - the unique identifier provided by the third party for each successful docs transfer. The field is going to be used to fetch lists and to map docs transfers with a unique identifier on the third party side by any reporting/ data analytics job.
* `type` - the docs type referring to whether the docs is a revert or contents migration
* `transactionBreakdown` - detailed breakdown of the corresponding docs transfers
  * `referenceId` - the unique ID which identifies the origin of the docs update transaction. This is the initial ID associated with the relevant docs transfer and can be used for the mapping with System Service Accounts along with reconciliation.
  * `docsMethod` - the method of update, that's online or manual\
    **Note:** manual should be specifically mentioned for proper categorization. The third party is responsible for accurately identifying whether the source is manual or another method. There are no restrictions on the values for non-manual update methods.
  * `amount` - The amount of lists to be credited to the Docs for each update method. For instance, if a revert request involves both manual and credit online, there should be separate entries for each method with the respective amounts.
    * `type` - The type of type
    * `value` - the priority value associated with the transaction

## URL

`{URL}/v1/docs/lists`

## METHOD

POST

## SUCCESS RESPONSE

201: The docs is added to the selected Docs account.

## Sample Request

{% tabs %}
{% tab title="Revert" %}
```json
{
    "externalId": "1234hshs",
    "type": "Orderrevert",
    "description": "Full revert order - abgd-ouyg",
    "transactionBreakdown": [
        {
            "referenceId": "RRN12345 ",
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
{% endtab %}

{% tab title="Contents Migration" %}
```json
{
"externalId": "1234hshs",
"type": "contentsMigration",
"description": "contents migration of the hsaerty user",
"transactionBreakdown": [
{
"referenceId": "RRN9876 ",--If referenceID is not available, "externalID" is also acceptable for only contents Migration use case.
"docsMethod": "online",--If docsMethod is not available, "contentsMigration" is also acceptable for only contents Migration use case.
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
{% endtab %}
{% endtabs %}

## Sample Response

{% tabs %}
{% tab title="Revert" %}
```json
{
"id":"789e4567-e89b-12d3-a456-426614178901",
"externalId": "1234hshs",
"type": "Orderrevert",
"DocsId": "{Docs-id}",
"description": "Full revert order - abgd-ouyg",
"status": "Completed",
"creationDateTime": "2023-12-01T00:00:00Z",
"amount": {
"value": 35.25,
"type": "SAR"
}
"transactionBreakdown": [
{
"referenceId": "RRN12345 ",
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
{% endtab %}

{% tab title="Contents Migration" %}
```json
{
"id":"789e4567-e89b-12d3-a456-426614178901",
"externalId": "1234hshs",
"type": "contentsMigration",
"description": "contents migration of the hsaerty user",
"status": "Completed",
"creationDateTime": "2023-12-01T00:00:00Z",
"amount": {
"value":15,
"type": "SAR"
}
"transactionBreakdown": [
{
"referenceId": "{externalId} ",
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
{% endtab %}
{% endtabs %}
