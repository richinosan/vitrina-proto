# Lint proto definitions

Lint lets a contract author validate both modules against the repository's Buf rules before publishing API changes.

## Sub-features

- `lint-all` runs `buf lint` for `event` and `organization` through the workspace config.
- `lint-clean` confirms no lint findings are emitted on a clean checkout.
- `lint-fail` would surface rule violations when a `.proto` file breaks STANDARD lint rules.

## How to get to it (user POV)

- Run `mise run lint` from the repository root after editing any `.proto` file.
- Run the same command locally before opening a pull request that changes contracts.

## Driving it with verify-vitrina-proto

Preconditions:

- `verify-vitrina-proto launch` completed successfully.
- `verify-vitrina-proto doctor` reports `doctor: ready`.
- `VITRINA_VERIFY_RUN_ID` is set to a unique value.

- **Workspace lint.** Run the repo lint task. Run `verify-vitrina-proto drive lint-proto`. Exit code `0` and `lint.exit.txt` contain `0`.
- **Lint output.** Inspect captured stdout. Read `evidence/<run-id>/lint.stdout.txt`. The file is empty or contains only informational output; stderr is empty on success.
- **Config snapshot.** Confirm the workspace config used for lint. Read `evidence/<run-id>/buf.yaml.snapshot`. It matches the root `buf.yaml` checked into the repo.
- **Proof.** Keep `run.meta.json`, `lint.cmd.txt`, `lint.stdout.txt`, `lint.stderr.txt`, and `lint.exit.txt`. They show the exact command and a zero exit from `mise run lint`.

## Gotchas

- `buf lint` reads the workspace `buf.yaml`; do not lint a single module in isolation unless the feature explicitly says so.
- Lint failures exit non-zero. A non-empty stderr file with exit code `1` is expected failure evidence, not a harness bug.
- Doctor must pass before driving. Missing `mise` tools produces a doctor failure, not a lint failure.
- Do not rewrite `.proto` files during a read-only verification run.
