# Organization contract surface

Organization contract surface lets an integrator confirm the `organization.v1` module compiles and exposes the expected Organization read API.

## Sub-features

- `organization-build` compiles the `organization` module into a Buf image.
- `organization-service-rpcs` confirms `OrganizationService` exposes `GetOrganization` and `ListOrganizations`.
- `organization-image-size` records the built image size as a sanity check that output was produced.

## How to get to it (user POV)

- Review `organization/organization/v1/api.proto` when integrating with `organization.v1.OrganizationService`.
- Build the module locally before publishing generated stubs or updating downstream services.

## Driving it with verify-vitrina-proto

Preconditions:

- `verify-vitrina-proto launch` completed successfully.
- `verify-vitrina-proto doctor` reports `doctor: ready`.
- `VITRINA_VERIFY_RUN_ID` is set to a unique value.

- **Build module.** Compile the organization module. Run `verify-vitrina-proto drive organization-contract`. Exit code `0`.
- **Build proof.** Read `build.exit.txt` and `build.stderr.txt`. Exit code `0` with empty stderr means `buf build organization` succeeded.
- **Image proof.** Read `image-size.stdout.txt`. It contains a non-zero byte count for the generated Buf image.
- **RPC listing.** Read `organization-service.rpcs.txt`. It lists `OrganizationService`, `GetOrganization`, and `ListOrganizations` from `organization/organization/v1/api.proto`.
- **Proof.** Keep `run.meta.json`, build transcripts, `image-size.*`, and `organization-service.rpcs.txt`.

## Gotchas

- This feature proves compile-time contract surface, not runtime RPC behavior. Do not call private ConnectRPC endpoints from this skill.
- Organization images and caller permissions are part of the module but are not separately asserted by the default RPC listing file.
- The built image is written under `/tmp/vitrina-proto-verify-<run-id>/`; cleanup removes it while evidence remains.
- Alias resolution rules for `organizations/{id}` names are documented in proto comments; this harness does not execute those rules against live data.
