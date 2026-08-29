# vitrina-proto verification map

This directory is the maintained source for verifying contract-author behavior in vitrina-proto. Read this index before driving the repo, then open the matching feature file as the recipe.

## Baseline preconditions

- Work from the repository root that contains `buf.yaml`.
- Run `.cursor/skills/verify-vitrina-proto/helpers/verify-vitrina-proto launch` once per verification run.
- Set `VITRINA_VERIFY_RUN_ID` to a unique value so concurrent runs do not share scratch directories.
- Put `.cursor/skills/verify-vitrina-proto/helpers` on `PATH` or call the helper with its full path.
- Run `verify-vitrina-proto doctor` and require `doctor: ready`.
- Do not modify committed `.proto` files during read-only verification.

## Driving conventions

- Start every recipe from the baseline state unless its preconditions say otherwise.
- Run repo commands through `mise exec --` or `mise run` exactly as CI does.
- Treat every command in a feature file as literal.
- Use module names `event` and `organization`, not guessed package paths.
- Restore any intentional scratch edits during cleanup. Do not remove proof artifacts during cleanup.

## Proof and skip reporting

- Capture the command, stdout, stderr, and exit code for each driven step.
- Lint proof includes a zero exit from `mise run lint`.
- Docs proof includes regenerated README output and whether it matches committed files.
- Breaking proof includes the `mise run breaking` result or an explicit skip reason when `origin/main` has no `.proto` files.
- Contract proof includes a built Buf image for the module and a file listing expected RPC names.
- Record the feature ID and entry point used in `run.meta.json` and keep artifacts under `.cursor/skills/verify-vitrina-proto/evidence/<VITRINA_VERIFY_RUN_ID>/`.
- Report an unreachable path with the attempted command and the unmet precondition.
- Do not report a skipped entry point as verified through a different path.

## Feature entry contract

Each feature file starts with an H1 title and one paragraph describing the user-visible behavior. It then uses exactly four H2 sections in this order.

1. `Sub-features` lists short IDs with one line for each behavior.
2. `How to get to it (user POV)` lists every user entry point.
3. `Driving it with verify-vitrina-proto` starts with `Preconditions:` and uses labeled bullets that pair each user action with an exact command and observable result.
4. `Gotchas` lists traps that can waste or invalidate a verification run.

Keep implementation details out of the map. Name only user paths, stable handles, required state, commands, and observable proof.

## Features

- [Lint proto definitions](./lint-proto.md) covers `buf lint` across both modules.
- [Generate protocol docs](./generate-docs.md) covers `mise run docs` and README drift detection.
- [Breaking change check](./breaking-check.md) covers `mise run breaking` against `origin/main`.
- [Event contract surface](./event-contract.md) covers compiling `event.v1` and verifying `EventService` RPCs.
- [Organization contract surface](./organization-contract.md) covers compiling `organization.v1` and verifying `OrganizationService` RPCs.
