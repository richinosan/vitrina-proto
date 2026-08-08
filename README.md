# vitrina-proto

Vitrina の public API contract を管理する repository です。

## Packages

```text
vitrina.event.v1
vitrina.organization.v1
```

## Resources

| Package | Resource | RPC |
|---|---|---|
| `vitrina.event.v1` | `PublicEvent` | `GetEvent`, `ListEvents` |
| `vitrina.organization.v1` | `PublicOrganization` | `GetOrganization`, `ListOrganizations` |

## ドキュメント

各 package 配下の `README.md` を `mise run generate` で生成します。

- `vitrina/event/v1/README.md`
- `vitrina/organization/v1/README.md`

## 開発

```bash
mise run lint
mise run generate
mise run breaking
mise run check
```
