# vitrina-proto

Vitrina の public API contract を管理する repository です。

## Package

```text
vitrina.v1
```

## Resources

| Resource | RPC |
|---|---|
| `PublicEvent` | `GetEvent`, `ListEvents` |
| `PublicOrganization` | `GetOrganization`, `ListOrganizations` |

## ドキュメント

`PROTO.md` は `mise run generate` で生成します。

## 開発

```bash
mise run lint
mise run generate
mise run breaking
mise run check
```
