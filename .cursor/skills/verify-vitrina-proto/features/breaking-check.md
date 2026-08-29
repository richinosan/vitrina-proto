# Breaking change check

Breaking check lets a contract author compare the current branch against `origin/main` and detect file-level breaking proto changes.

## Sub-features

- `breaking-run` executes `mise run breaking` when `origin/main` contains `.proto` files.
- `breaking-clean` confirms no breaking changes against `origin/main` on a compatible branch.
- `breaking-skip` records when breaking is skipped because `origin/main` has no proto history yet.

## How to get to it (user POV)

- Run `mise run breaking` from the repository root before merging contract changes.
- Run `mise run check` when lint, docs, and breaking must all pass together.

## Driving it with verify-vitrina-proto

Preconditions:

- `verify-vitrina-proto launch` completed successfully.
- `verify-vitrina-proto doctor` reports `doctor: ready`.
- `git fetch origin main` completed so `origin/main` is current.
- `VITRINA_VERIFY_RUN_ID` is set to a unique value.

- **Breaking run.** Execute the breaking task. Run `verify-vitrina-proto drive breaking-check`. Exit code `0`.
- **Mode marker.** Read `evidence/<run-id>/breaking.mode.txt`. It contains `ran` when breaking executed, or a skip reason when `origin/main` has no `.proto` files.
- **Breaking output.** When mode is `ran`, read `breaking.stdout.txt`, `breaking.stderr.txt`, and `breaking.exit.txt`. Exit code `0` means no breaking changes detected under the repo's FILE rules.
- **Proof.** Keep the breaking command transcript and `breaking.mode.txt`. They prove whether breaking ran and what it returned.

## Gotchas

- Breaking requires git history. Fetch `origin/main` before driving; stale refs produce misleading results.
- The repo uses `buf breaking --against '.git#ref=origin/main'`. Do not substitute another ref unless the task explicitly changes compatibility policy.
- A branch that intentionally introduces breaking changes exits non-zero; that is valid failure evidence, not a harness error.
- When `breaking.mode.txt` records a skip, report the feature as skipped-not-verified rather than as passing breaking compatibility.
