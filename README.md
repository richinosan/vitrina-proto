# vitrina-proto

Vitrina の **public API contract** を管理する repository です。

admin / internal API とは分離し、他サービス（CMS / SNS 等）が依存可能な read-oriented contract のみを公開します。

## Package

```text
party.kanade.vitrina.v1
```

## Public Resources

| Resource | RPC |
|---|---|
| `PublicEvent` | `GetEvent`, `ListEvents` |
| `PublicOrganization` | `GetOrganization`, `ListOrganizations` |

## Public に含めないもの

以下は admin / internal contract（`richinosan/vitrina` リポジトリ内 proto）に残します。

* RBAC (`Role`, `Permission`, `RoleAssignment`)
* `SchemaPublicationSettings` / `hidden_properties`
* Event / Organization の mutation RPC
* `Person` / 認証コンテキスト
* audit / internal status / administrative metadata

## Backend 実装状況

| RPC | vitrina backend |
|---|---|
| `GetEvent` | 未実装（public read service として今後追加） |
| `ListEvents` | 未実装 |
| `GetOrganization` | 未実装（Organization domain 未実装） |
| `ListOrganizations` | 未実装 |

本 repository は contract の正本です。RPC endpoint の認証要否は Backend 実装側で決定します。

```text
public proto != anonymous public endpoint
```

## Lint

```bash
mise run lint
```
