# Generate protocol docs

Generate docs lets a contract author regenerate module README files from `.proto` sources and confirm committed docs are up to date.

## Sub-features

- `docs-generate` runs `mise run docs` for both `event` and `organization`.
- `docs-up-to-date` confirms generated README files match committed output.
- `docs-drift` captures a git diff when generated docs differ from committed files.

## How to get to it (user POV)

- Run `mise run docs` from the repository root after changing messages, services, or comments that affect generated docs.
- Run `mise run check` before merge when CI must prove docs, lint, and breaking checks together.

## Driving it with verify-vitrina-proto

Preconditions:

- `verify-vitrina-proto launch` completed successfully.
- `verify-vitrina-proto doctor` reports `doctor: ready`.
- `VITRINA_VERIFY_RUN_ID` is set to a unique value.

- **Generate docs.** Run the docs task. Run `verify-vitrina-proto drive generate-docs`. Exit code `0` and `docs.exit.txt` contain `0`.
- **Up-to-date check.** Read `evidence/<run-id>/docs.up-to-date.txt`. On a clean checkout it begins with `ok:`; a drift message means regeneration changed `event/README.md` or `organization/README.md`.
- **Drift patch.** When drift exists, inspect `evidence/<run-id>/docs.diff.patch` for the exact README changes.
- **Proof.** Keep the docs command transcript files plus `docs.up-to-date.txt`. They prove generation succeeded and whether committed docs matched the generator output.

## Gotchas

- `mise run docs` writes into `event/README.md` and `organization/README.md`. The helper compares against pre-run copies; unexpected local edits before the drive can look like generator drift.
- A successful generator run with drift still exits `0`; read `docs.up-to-date.txt`, not exit code alone.
- CI fails when committed docs are stale. A drift patch is evidence to commit regenerated README files, not proof that verification passed.
- Cleanup removes scratch copies under `/tmp/vitrina-proto-verify-<run-id>/`; it does not revert README files in the repo.
