---
name: verify-vitrina-proto
description: "Drive vitrina-proto locally as a contract author would: install buf tooling with mise, run lint/docs/breaking checks, and prove event.v1 and organization.v1 compile. Use when verifying proto changes, generated docs drift, or CI-equivalent checks without deploying services."
---

# Verify vitrina-proto

This repository is a ConnectRPC contract surface, not a running service. Verification means driving the same local toolchain a contract author uses: `mise`, `buf lint`, `buf generate`, and `buf breaking`. There is no browser, no API server, and no production deploy in this skill.

Read `.cursor/skills/verify-vitrina-proto/features/README.md` before driving. Pick the feature file that matches the user-facing behavior under test, then follow its recipe through the helper.

## Launch

Install the repo's pinned tools once per verification run:

```bash
export PATH="$HOME/.local/bin:$PATH"
.cursor/skills/verify-vitrina-proto/helpers/verify-vitrina-proto launch
```

Ready when the command prints `launch: mise tools installed` and `mise exec -- buf --version` reports `1.72.0`.

There is no long-lived server. Each drive runs commands and exits. Teardown for a run is `cleanup` (below), not a process stop.

Optional run identifier:

```bash
export VITRINA_VERIFY_RUN_ID="20260829T112100Z"
```

## Doctor

Run this before the first drive and again after any failed drive:

```bash
export PATH="$HOME/.local/bin:$PATH"
.cursor/skills/verify-vitrina-proto/helpers/verify-vitrina-proto doctor
```

Require exit code `0` and the final line `doctor: ready`. Doctor checks:

- repo root contains `buf.yaml`
- `event/` and `organization/` modules exist
- `mise`, `buf`, and `protoc-gen-doc` are available
- the helper script is executable

Refuse to drive when doctor fails.

## Drive

Use the helper and the matching feature file in `features/`. Prefer stable handles from this repo:

- mise tasks: `lint`, `docs`, `breaking`, `check`
- modules: `event`, `organization`
- packages: `event.v1`, `organization.v1`
- service RPC names in `event/event/v1/api.proto` and `organization/organization/v1/api.proto`

Example for one feature:

```bash
export PATH="$HOME/.local/bin:$PATH"
export VITRINA_VERIFY_RUN_ID="20260829T112100Z"
.cursor/skills/verify-vitrina-proto/helpers/verify-vitrina-proto drive lint-proto
```

Supported feature IDs:

- `lint-proto`
- `generate-docs`
- `breaking-check`
- `event-contract`
- `organization-contract`

Drive the real user path from the feature map. Do not edit `.proto` files during verification unless the task explicitly requires a contract change. Do not call production services.

## Evidence

Evidence for a run lives at:

```text
.cursor/skills/verify-vitrina-proto/evidence/<VITRINA_VERIFY_RUN_ID>/
```

Print the active path:

```bash
.cursor/skills/verify-vitrina-proto/helpers/verify-vitrina-proto evidence-path
```

Proof standards for this repo:

- Exercise the same commands CI runs (`mise run lint`, `mise run docs`, `mise run breaking`) or the module build path for contract features.
- Capture both the command transcript and the observable result: exit code files, stdout/stderr captures, build artifact size, RPC listing, or docs drift diff.
- For docs generation, compare regenerated README output against committed files; a diff patch is evidence of drift, not proof of success.
- For contract features, a zero exit from `buf build <module>` plus the RPC listing file proves the module compiles and the expected service surface is present.
- Record the feature ID in `run.meta.json`.

The helper writes:

- `run.meta.json`
- `<step>.cmd.txt`, `<step>.stdout.txt`, `<step>.stderr.txt`, `<step>.exit.txt`
- feature-specific files such as `event-service.rpcs.txt` or `docs.diff.patch`

## Cleanup

Remove scratch state created during the run. Never delete evidence.

```bash
export VITRINA_VERIFY_RUN_ID="20260829T112100Z"
.cursor/skills/verify-vitrina-proto/helpers/verify-vitrina-proto cleanup
```

Cleanup removes `/tmp/vitrina-proto-verify-<VITRINA_VERIFY_RUN_ID>/` (or `$TMPDIR` equivalent). Evidence under `.cursor/skills/verify-vitrina-proto/evidence/<VITRINA_VERIFY_RUN_ID>/` must remain after cleanup.

Never kill processes by name. This repo's verification does not start background servers.

## Helpers

Primary harness:

```bash
.cursor/skills/verify-vitrina-proto/helpers/verify-vitrina-proto help
```

Commands:

| Command | Purpose |
| --- | --- |
| `launch` | `mise install` for pinned tools |
| `doctor` | read-only readiness check |
| `drive <feature-id>` | run one mapped feature and write evidence |
| `evidence-path` | print evidence directory |
| `cleanup` | remove scratch only |

Put the helper on `PATH` when driving many features in one shell:

```bash
export PATH="$PWD/.cursor/skills/verify-vitrina-proto/helpers:$PATH"
verify-vitrina-proto doctor
```

Maintenance loop: use `/maintain-verification-skill` when app behavior or CI tasks change.
