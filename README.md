# Project V2 Sync

Keep GitHub Issues from multiple repositories reconciled into one GitHub
Project V2.

> Status: `v0.1-beta`

Project V2 Sync is a focused extraction of a reconciliation pattern proven in
a larger GitHub operations stack. It is useful when the Project should be the
consolidated operational view while Issues remain owned by their technical
repositories.

## Core rule

```text
Issue exists in configured repository
        +
repository is managed
        =
Issue belongs in configured Project V2
```

Metadata is optional. It classifies fields; it does not gate admission.

## Features

- Project owner may be a GitHub user or organization;
- configurable Project number;
- multiple managed repositories;
- REST pagination for repository Issues;
- complete GraphQL pagination for `ProjectV2.items`;
- optional metadata block;
- configurable Status / Project / Repository / Operator / date fields;
- optional automatic creation of helper TEXT fields;
- closed Issues force the configured completion status;
- scheduled and manual reconciliation.

## Example metadata

```html
<!-- PROJECT_SYNC
project=Platform
status=In Progress
operator=Automation
start_date=2026-09-22
target_date=2026-09-30
-->
```

## Quick start

1. Copy `project-sync.example.json` to `project-sync.json`.
2. Set GitHub Actions secret `PROJECT_SYNC_TOKEN`.
3. Copy `templates/project-sync.yml` into `.github/workflows/`.
4. Copy `scripts/project_sync.py`.
5. Run the workflow manually once and inspect the reconciliation log.

## Pagination contract

The product follows `pageInfo.hasNextPage/endCursor` until the complete
Project item connection has been read. It never treats `first:100` as the
complete Project.

## Security

The synchronizer only performs the configured Project reconciliation mutations.
It does not edit Issue bodies, close/reopen Issues or change repository
settings.

See [Security](docs/SECURITY.md) and [Architecture](docs/ARCHITECTURE.md).

## Development

```bash
python3 -m py_compile scripts/project_sync.py
python3 -m unittest discover -s tests -p 'test_*.py' -v
```

## License

MIT
