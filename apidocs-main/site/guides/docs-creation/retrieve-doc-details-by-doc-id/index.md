# index

This request retrieves the details of a specific Docs by the Docs ID. The details are retrieved using the following:

Each Doc created in the Docs ecosystem is assigned a unique internal identifier. This endpoint allows you to retrieve the full details of a Doc using that identifier.

You can use this API to:

* Verify the status of a Doc
* Retrieve ownership information
* Validate Doc existence before performing updates
* Display Doc details in customer dashboards

***

## When to Use This Endpoint

Use this API when you need to:

* Display Doc details in an application
* Verify whether a Doc is active, locked, or terminated
* Confirm ownership of a Doc
* Perform pre-checks before updating a Doc

***

## Prerequisites

Before calling this API, ensure you have:

### Query parameters - Required

* `id` - the unique identifier created by Docs Service for each Docs object
* `Docs-Entity-ID` - the unique identifier of the third party entity

The retrieved response displays the details associated with the specified Docs ID.
