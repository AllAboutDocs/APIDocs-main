# index

This request retrieves the current Docs contents and other contents that will expire soon for a specific Docs ID. The details are retrieved using the following:

Each Docs object contains one or more content records associated with user activity. This endpoint allows you to:

* View aggregated contents
* View account-level contents
* Identify content that is nearing expiration

This is commonly used for:

* Customer dashboards
* Compliance monitoring
* Expiry notifications
* Reporting and reconciliation

## When to Use This Endpoint

Use this API when you need to:

* Display all active contents for a Doc
* Track upcoming content expirations
* Perform compliance or regulatory tracking
* Show user-specific content summaries

## Prerequisites

Before making this request, ensure you have:

### Query parameters - Required

* `id` - the unique internal identifier for the Docs
* `Docs-Entity-ID` - the unique identifier of the third party entity

The retrieved response displays the details associated with the specified Docs ID.
