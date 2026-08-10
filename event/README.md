# Protocol Documentation
<a name="top"></a>

## Table of Contents

- [event/v1/event.proto](#event_v1_event-proto)
    - [Event](#event-v1-Event)
    - [EventSummary](#event-v1-EventSummary)
  
- [event/v1/event_api.proto](#event_v1_event_api-proto)
    - [GetEventRequest](#event-v1-GetEventRequest)
    - [ListEventsRequest](#event-v1-ListEventsRequest)
    - [ListEventsResponse](#event-v1-ListEventsResponse)
  
- [event/v1/rbac.proto](#event_v1_rbac-proto)
    - [Permission](#event-v1-Permission)
    - [Role](#event-v1-Role)
    - [RoleAssignment](#event-v1-RoleAssignment)
  
    - [RoleAssignmentScopeType](#event-v1-RoleAssignmentScopeType)
  
- [event/v1/rbac_api.proto](#event_v1_rbac_api-proto)
    - [GetPermissionRequest](#event-v1-GetPermissionRequest)
    - [GetRoleAssignmentRequest](#event-v1-GetRoleAssignmentRequest)
    - [GetRoleRequest](#event-v1-GetRoleRequest)
    - [ListPermissionsRequest](#event-v1-ListPermissionsRequest)
    - [ListPermissionsResponse](#event-v1-ListPermissionsResponse)
    - [ListRoleAssignmentsRequest](#event-v1-ListRoleAssignmentsRequest)
    - [ListRoleAssignmentsResponse](#event-v1-ListRoleAssignmentsResponse)
    - [ListRolesRequest](#event-v1-ListRolesRequest)
    - [ListRolesResponse](#event-v1-ListRolesResponse)
  
- [event/v1/api.proto](#event_v1_api-proto)
    - [EventService](#event-v1-EventService)
    - [PermissionService](#event-v1-PermissionService)
    - [RoleAssignmentService](#event-v1-RoleAssignmentService)
    - [RoleService](#event-v1-RoleService)
  
- [Scalar Value Types](#scalar-value-types)



<a name="event_v1_event-proto"></a>
<p align="right"><a href="#top">Top</a></p>

## event/v1/event.proto



<a name="event-v1-Event"></a>

### Event
Event は Event リソースの公開表現。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| id | [string](#string) |  |  |
| schema_type | [string](#string) |  |  |
| name | [string](#string) |  |  |
| description | [string](#string) |  |  |
| start_date | [string](#string) |  |  |
| end_date | [string](#string) |  |  |
| location_json | [string](#string) |  |  |
| event_attendance_mode | [string](#string) |  |  |
| event_status | [string](#string) |  |  |
| image | [string](#string) |  |  |
| url | [string](#string) |  |  |
| organizer_organization_id | [string](#string) |  | organizer として紐付ける Organization の id (organizations/{id} の {id} 部分)。 |
| parent | [EventSummary](#event-v1-EventSummary) |  |  |
| children | [EventSummary](#event-v1-EventSummary) | repeated |  |






<a name="event-v1-EventSummary"></a>

### EventSummary
EventSummary は親子関係の 1 階層埋め込み用。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| id | [string](#string) |  |  |
| schema_type | [string](#string) |  |  |
| name | [string](#string) |  |  |
| description | [string](#string) |  |  |
| start_date | [string](#string) |  |  |
| end_date | [string](#string) |  |  |
| location_json | [string](#string) |  |  |
| event_attendance_mode | [string](#string) |  |  |
| event_status | [string](#string) |  |  |
| image | [string](#string) |  |  |
| url | [string](#string) |  |  |
| organizer_organization_id | [string](#string) |  |  |





 

 

 

 



<a name="event_v1_event_api-proto"></a>
<p align="right"><a href="#top">Top</a></p>

## event/v1/event_api.proto



<a name="event-v1-GetEventRequest"></a>

### GetEventRequest
GetEventRequest はイベントを取得する。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| name | [string](#string) |  | name は events/{id} 形式。 |






<a name="event-v1-ListEventsRequest"></a>

### ListEventsRequest
ListEventsRequest はイベント一覧を取得する。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| page_size | [int32](#int32) |  |  |
| page_token | [string](#string) |  |  |






<a name="event-v1-ListEventsResponse"></a>

### ListEventsResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| events | [Event](#event-v1-Event) | repeated |  |
| next_page_token | [string](#string) |  |  |





 

 

 

 



<a name="event_v1_rbac-proto"></a>
<p align="right"><a href="#top">Top</a></p>

## event/v1/rbac.proto



<a name="event-v1-Permission"></a>

### Permission
Permission は resource &#43; action による権限。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| name | [string](#string) |  | リソース名（permissions/{id}）。 |
| id | [string](#string) |  |  |
| resource | [string](#string) |  |  |
| action | [string](#string) |  |  |






<a name="event-v1-Role"></a>

### Role
Role は Role 定義。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| name | [string](#string) |  | リソース名（roles/{id}）。 |
| id | [string](#string) |  |  |
| display_name | [string](#string) |  |  |
| description | [string](#string) |  |  |






<a name="event-v1-RoleAssignment"></a>

### RoleAssignment
RoleAssignment は Person への Role 割当。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| name | [string](#string) |  | リソース名（roleAssignments/{id}）。 |
| id | [string](#string) |  |  |
| person | [string](#string) |  | persons/{id} |
| role | [string](#string) |  | roles/{id} |
| scope_type | [RoleAssignmentScopeType](#event-v1-RoleAssignmentScopeType) |  |  |
| scope | [string](#string) |  | events/{id} または organizations/{id}。SYSTEM scope では未設定。 |
| person_kebab_identifier | [string](#string) |  | 割当先の kebab identifier(subject)。表示用。他サービスの AuthenticationService.GetUser(users/{person_kebab_identifier}) で プロフィールを解決できる。 |





 


<a name="event-v1-RoleAssignmentScopeType"></a>

### RoleAssignmentScopeType
RoleAssignmentScopeType は RoleAssignment の scope 種別。

| Name | Number | Description |
| ---- | ------ | ----------- |
| ROLE_ASSIGNMENT_SCOPE_TYPE_UNSPECIFIED | 0 |  |
| ROLE_ASSIGNMENT_SCOPE_TYPE_SYSTEM | 1 |  |
| ROLE_ASSIGNMENT_SCOPE_TYPE_EVENT | 2 |  |
| ROLE_ASSIGNMENT_SCOPE_TYPE_ORGANIZATION | 3 |  |


 

 

 



<a name="event_v1_rbac_api-proto"></a>
<p align="right"><a href="#top">Top</a></p>

## event/v1/rbac_api.proto



<a name="event-v1-GetPermissionRequest"></a>

### GetPermissionRequest
GetPermissionRequest は Permission を取得する。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| name | [string](#string) |  | リソース名（permissions/{id}）。 |






<a name="event-v1-GetRoleAssignmentRequest"></a>

### GetRoleAssignmentRequest
GetRoleAssignmentRequest は RoleAssignment を取得する。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| name | [string](#string) |  | リソース名（roleAssignments/{id}）。 |






<a name="event-v1-GetRoleRequest"></a>

### GetRoleRequest
GetRoleRequest は Role を取得する。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| name | [string](#string) |  | リソース名（roles/{id}）。 |






<a name="event-v1-ListPermissionsRequest"></a>

### ListPermissionsRequest
ListPermissionsRequest は Permission 一覧を取得する。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| page_size | [int32](#int32) |  |  |
| page_token | [string](#string) |  |  |






<a name="event-v1-ListPermissionsResponse"></a>

### ListPermissionsResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| permissions | [Permission](#event-v1-Permission) | repeated |  |
| next_page_token | [string](#string) |  |  |






<a name="event-v1-ListRoleAssignmentsRequest"></a>

### ListRoleAssignmentsRequest
ListRoleAssignmentsRequest は RoleAssignment 一覧を取得する。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| parent | [string](#string) |  | 親リソース（events/{id} または organizations/{id}）。 |
| page_size | [int32](#int32) |  |  |
| page_token | [string](#string) |  |  |






<a name="event-v1-ListRoleAssignmentsResponse"></a>

### ListRoleAssignmentsResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| role_assignments | [RoleAssignment](#event-v1-RoleAssignment) | repeated |  |
| next_page_token | [string](#string) |  |  |






<a name="event-v1-ListRolesRequest"></a>

### ListRolesRequest
ListRolesRequest は Role 一覧を取得する。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| page_size | [int32](#int32) |  |  |
| page_token | [string](#string) |  |  |






<a name="event-v1-ListRolesResponse"></a>

### ListRolesResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| roles | [Role](#event-v1-Role) | repeated |  |
| next_page_token | [string](#string) |  |  |





 

 

 

 



<a name="event_v1_api-proto"></a>
<p align="right"><a href="#top">Top</a></p>

## event/v1/api.proto


 

 

 


<a name="event-v1-EventService"></a>

### EventService
EventService は Event API を提供する。

| Method Name | Request Type | Response Type | Description |
| ----------- | ------------ | ------------- | ------------|
| GetEvent | [GetEventRequest](#event-v1-GetEventRequest) | [Event](#event-v1-Event) |  |
| ListEvents | [ListEventsRequest](#event-v1-ListEventsRequest) | [ListEventsResponse](#event-v1-ListEventsResponse) |  |


<a name="event-v1-PermissionService"></a>

### PermissionService
PermissionService は Permission の参照 API を提供する。

| Method Name | Request Type | Response Type | Description |
| ----------- | ------------ | ------------- | ------------|
| GetPermission | [GetPermissionRequest](#event-v1-GetPermissionRequest) | [Permission](#event-v1-Permission) |  |
| ListPermissions | [ListPermissionsRequest](#event-v1-ListPermissionsRequest) | [ListPermissionsResponse](#event-v1-ListPermissionsResponse) |  |


<a name="event-v1-RoleAssignmentService"></a>

### RoleAssignmentService
RoleAssignmentService は RoleAssignment の参照 API を提供する。

| Method Name | Request Type | Response Type | Description |
| ----------- | ------------ | ------------- | ------------|
| GetRoleAssignment | [GetRoleAssignmentRequest](#event-v1-GetRoleAssignmentRequest) | [RoleAssignment](#event-v1-RoleAssignment) |  |
| ListRoleAssignments | [ListRoleAssignmentsRequest](#event-v1-ListRoleAssignmentsRequest) | [ListRoleAssignmentsResponse](#event-v1-ListRoleAssignmentsResponse) |  |


<a name="event-v1-RoleService"></a>

### RoleService
RoleService は Role の参照 API を提供する。

| Method Name | Request Type | Response Type | Description |
| ----------- | ------------ | ------------- | ------------|
| GetRole | [GetRoleRequest](#event-v1-GetRoleRequest) | [Role](#event-v1-Role) |  |
| ListRoles | [ListRolesRequest](#event-v1-ListRolesRequest) | [ListRolesResponse](#event-v1-ListRolesResponse) |  |

 



## Scalar Value Types

| .proto Type | Notes | C++ | Java | Python | Go | C# | PHP | Ruby |
| ----------- | ----- | --- | ---- | ------ | -- | -- | --- | ---- |
| <a name="double" /> double |  | double | double | float | float64 | double | float | Float |
| <a name="float" /> float |  | float | float | float | float32 | float | float | Float |
| <a name="int32" /> int32 | Uses variable-length encoding. Inefficient for encoding negative numbers – if your field is likely to have negative values, use sint32 instead. | int32 | int | int | int32 | int | integer | Bignum or Fixnum (as required) |
| <a name="int64" /> int64 | Uses variable-length encoding. Inefficient for encoding negative numbers – if your field is likely to have negative values, use sint64 instead. | int64 | long | int/long | int64 | long | integer/string | Bignum |
| <a name="uint32" /> uint32 | Uses variable-length encoding. | uint32 | int | int/long | uint32 | uint | integer | Bignum or Fixnum (as required) |
| <a name="uint64" /> uint64 | Uses variable-length encoding. | uint64 | long | int/long | uint64 | ulong | integer/string | Bignum or Fixnum (as required) |
| <a name="sint32" /> sint32 | Uses variable-length encoding. Signed int value. These more efficiently encode negative numbers than regular int32s. | int32 | int | int | int32 | int | integer | Bignum or Fixnum (as required) |
| <a name="sint64" /> sint64 | Uses variable-length encoding. Signed int value. These more efficiently encode negative numbers than regular int64s. | int64 | long | int/long | int64 | long | integer/string | Bignum |
| <a name="fixed32" /> fixed32 | Always four bytes. More efficient than uint32 if values are often greater than 2^28. | uint32 | int | int | uint32 | uint | integer | Bignum or Fixnum (as required) |
| <a name="fixed64" /> fixed64 | Always eight bytes. More efficient than uint64 if values are often greater than 2^56. | uint64 | long | int/long | uint64 | ulong | integer/string | Bignum |
| <a name="sfixed32" /> sfixed32 | Always four bytes. | int32 | int | int | int32 | int | integer | Bignum or Fixnum (as required) |
| <a name="sfixed64" /> sfixed64 | Always eight bytes. | int64 | long | int/long | int64 | long | integer/string | Bignum |
| <a name="bool" /> bool |  | bool | boolean | boolean | bool | bool | boolean | TrueClass/FalseClass |
| <a name="string" /> string | A string must always contain UTF-8 encoded or 7-bit ASCII text. | string | String | str/unicode | string | string | string | String (UTF-8) |
| <a name="bytes" /> bytes | May contain any arbitrary sequence of bytes. | string | ByteString | str | []byte | ByteString | string | String (ASCII-8BIT) |

