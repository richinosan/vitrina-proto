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

各 module 配下の `README.md` を `mise run docs` で生成します。

- `eventapis/README.md`
- `organizationapis/README.md`

## 開発

```bash
mise run lint
mise run docs
mise run breaking
mise run check
```
