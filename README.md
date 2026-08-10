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

## TypeScript の生成物と配布

`mise run generate`(`mise run docs` のエイリアス)を実行すると、各 module 配下に
`protoc-gen-es`(`target=ts`)で生成した TypeScript(`<module>/gen/es/**`)も出力されます。
`gen/es/` はリポジトリにコミットしません(利用側で都度生成する前提のため)。

このリポジトリの proto を利用する方法は主に2通りあります。

1. **このリポジトリを直接参照して生成する**: このリポジトリを clone し、`mise run generate`
   (内部的には `buf generate`。プラグインは `@bufbuild/protoc-gen-es@2.12.1`)を実行して
   `<module>/gen/es/**` を得る。依存先で `@bufbuild/protobuf` / `@connectrpc/connect` が必要。
2. **raw な `.proto` を自分のリポジトリに取り込んで生成する**(private な vitrina / kebab が
   採用している方法): `rsync` 等で `.proto` ファイルのみをコピーし、取り込み側の
   `buf generate` 設定で生成する。取り込み側で admin 専用フィールドの追加など独自の後処理が
   必要な場合はこちらが適する。

いずれの方法でも、生成対象には Event の Get / List(`event_api.proto`)、閲覧権限モデル
(`event_permission.proto`)を含む、このリポジトリ配下の全 `.proto` が含まれます。

## 開発

```bash
mise run lint
mise run docs
mise run breaking
mise run check
```
