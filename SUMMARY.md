# Table of contents

* [Introduction](README.md)

## Docs Creation and Management APIs

* [Create a New Doc](docs-creation/create-a-new-doc.md)
* [Retrieve Doc Details by Doc ID](docs-creation/retrieve-doc-details-by-doc-id.md)
* [List Doc Contents and Expiring Contents](docs-creation/list-doc-content-and-expiring-content-by-doc-id.md)
* [Update Doc Status](docs-creation/update-doc-status.md)

## Docs Update via Lists APIs

* [Add Lists through Relists](docs-update-via-lists/add-lists-through-relists-or-content-migration.md)
* [Cancel a Specific Doc](docs-update-via-lists/cancel-a-specific-doc.md)

## API Reference

* [OpenAPI Specification](api-reference/README.md)
* ```yaml
  type: builtin:openapi
  props:
    models: true
    downloadLink: true
  dependencies:
    spec:
      ref:
        kind: openapi
        spec: new-org-api
  ```
