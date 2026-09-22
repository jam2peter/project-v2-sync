# Architecture

Project V2 Sync is a reconciliation loop.

```text
versioned config
  -> discover configured repositories
  -> enumerate every Issue (REST pagination)
  -> enumerate every Project item (GraphQL cursor pagination)
  -> add missing Issue items
  -> normalize metadata/labels
  -> update configured fields
  -> log sanitized reconciliation evidence
```

The Project is a consolidated view, not the source repository for Issue
content. Metadata is classification input, not an admission gate.
