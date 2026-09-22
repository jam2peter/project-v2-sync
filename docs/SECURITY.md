# Security

Store the GitHub credential only as the Actions secret
`PROJECT_SYNC_TOKEN`.

Use the minimum GitHub permissions that allow reading the configured Issues and
reading/updating the configured Project V2.

Project V2 Sync does not edit Issue bodies, close or reopen Issues, change
repository settings, administer secrets, or expose a generic GraphQL proxy.

Public examples contain only synthetic owners, repositories and Project
numbers.
