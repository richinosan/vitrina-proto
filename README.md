# vitrina-proto

Vitrina の public API contract を管理する repository です。

## Packages

```text
event.public.v1
organization.public.v1
```

## Resources

| Package | Resource | RPC |
|---|---|---|
| `event.public.v1` | `PublicEvent` | `GetEvent`, `ListEvents` |
| `organization.public.v1` | `PublicOrganization` | `GetOrganization`, `ListOrganizations` |

## ドキュメント

各 package 配下の `README.md` を `mise run generate` で生成します。

- `event/public/v1/README.md`
- `organization/public/v1/README.md`

## 開発

```bash
mise run lint
mise run generate
mise run breaking
mise run check
```
