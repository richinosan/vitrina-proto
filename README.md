# vitrina-proto

Vitrina の public API contract を管理する repository です。

ConnectRPC の URL は private 実装と同一です（例: `/event.v1.EventService/GetEvent`）。

## Packages

```text
event.v1
organization.v1
```

## Resources

| Package | Resource | RPC |
|---|---|---|
| `event.v1` | `Event` | `GetEvent`, `ListEvents` |
| `organization.v1` | `Organization` | `GetOrganization`, `ListOrganizations` |

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
