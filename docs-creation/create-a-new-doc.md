# create a new doc

This request creates a new Docs account in the Docs ecosystem and establishes a docs container for a user. A user can have one or more docs, each identified by a unique Docs ID, linked user ID, and type. Testing the PR workflow now.

A Docs object represents a user's document container.

When you call this endpoint:

* If the **user does not exist**, a new user is created automatically using `externalId` and then passing the `X-User-Id` value in the header during Docs creation.
* If the **user already exists**, the Docs object links to an existing `owner.id`. You must provide **either**: `owner.id` or `externalId`

## When to Use This Endpoint

Use this API when:

* onboarding a new customer
* creating a Docs container for an existing customer
* linking third-party customer identifiers using `externalId`
* setting up onboarding flows that require Docs

## Prerequisites

Ensure you have the following before making a request:

### Query Parameters - Required\*

* `Docs-Entity-ID` - the unique identifier of the third party entity
* `X-Idempotency-Key` - the unique server-created key to confirm subsequent retries of the same request

### Request Parameters - Required\*

* `type` - the type of the Docs to be created
* `owner`
  * `id` - the unique ID of the Docs owner
* `externalId` - the unique customer code of of Docs user
