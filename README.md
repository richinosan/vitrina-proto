# vitrina-proto

Vitrina の public API contract を管理する repository です。

サイト表示用ではなく、適切な権限を持つ別サービスとの連携用です。ConnectRPC の URL は private 実装と同一です（例: `/event.v1.EventService/GetEvent`）。

## Packages

```text
event.v1
organization.v1
```

`event.v1` には Event 参照と RBAC 参照（Get / List のみ）を含めます。

## Layout

```text
event/
  buf.gen.yaml
  event/v1/*.proto
organization/
  buf.gen.yaml
  organization/v1/*.proto
```

## ドキュメント

各 module 配下の `README.md` を `mise run docs` で生成します。

## 開発

```bash
mise run lint
mise run docs
mise run breaking
mise run check
```
