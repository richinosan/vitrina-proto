# Event contract surface

Event contract surface lets an integrator confirm the `event.v1` module compiles and exposes the expected read-only Event and RBAC services.

## Sub-features

- `event-build` compiles the `event` module into a Buf image.
- `event-service-rpcs` confirms `EventService` exposes `GetEvent` and `ListEvents`.
- `event-image-size` records the built image size as a sanity check that output was produced.

## How to get to it (user POV)

- Review `event/event/v1/api.proto` when integrating with `event.v1.EventService` or RBAC read services.
- Build the module locally before publishing generated stubs or updating downstream services.

## Driving it with verify-vitrina-proto

Preconditions:

- `verify-vitrina-proto launch` completed successfully.
- `verify-vitrina-proto doctor` reports `doctor: ready`.
- `VITRINA_VERIFY_RUN_ID` is set to a unique value.

- **Build module.** Compile the event module. Run `verify-vitrina-proto drive event-contract`. Exit code `0`.
- **Build proof.** Read `build.exit.txt` and `build.stderr.txt`. Exit code `0` with empty stderr means `buf build event` succeeded.
- **Image proof.** Read `image-size.stdout.txt`. It contains a non-zero byte count for the generated Buf image.
- **RPC listing.** Read `event-service.rpcs.txt`. It lists `EventService`, `GetEvent`, and `ListEvents` from `event/event/v1/api.proto`.
- **Proof.** Keep `run.meta.json`, build transcripts, `image-size.*`, and `event-service.rpcs.txt`.

## Gotchas

- This feature proves compile-time contract surface, not runtime RPC behavior. Do not call private ConnectRPC endpoints from this skill.
- RBAC services (`RoleService`, `PermissionService`, `RoleAssignmentService`) live in the same module but are not asserted by the default RPC listing file; extend proof manually if those services are in scope.
- The built image is written under `/tmp/vitrina-proto-verify-<run-id>/`; cleanup removes it while evidence remains.
- A missing import or syntax error fails `buf build` with non-zero exit code before RPC listing is produced.
