# index

This request updates the Docs status. Each Doc in the Docs ecosystem operates under a specific status that determines its availability and behavior. This endpoint allows you to change the status of a Doc using a PATCH operation. The various Docs statuses are described below:

* **Active** - The Docs account is active and is fully operational. All Docs activity is operational.
* **Pending** - The Docs account is pending and is partially operational. Docs activity related to lists will be pending.
* **Blocked** - The Docs account is blocked and is fully non-operational.

***

## When to Use This Endpoint

Use this API when you need to:

* Activate a newly created Doc
* Temporarily suspend a Doc
* Block access to a Doc for compliance or security reasons
* Resume Doc operations after review

***

## Prerequisites

Before updating a Doc’s status, ensure you have:

### Query parameters - Required

* `id` - the unique internal identifier of the Docs to update
* `Docs-Entity-ID` - the unique identifier of the third party entity

### Request Parameters - Required

* `path` - the property to be updated, e.g. status
* `op` - the operation to be performed, e.g. replace
* `value` - the status to be applied, e.g. block
