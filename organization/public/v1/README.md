# Protocol Documentation
<a name="top"></a>

## Table of Contents

- [organization/public/v1/organization.proto](#organization_public_v1_organization-proto)
    - [PublicOrganization](#organization-public-v1-PublicOrganization)
  
- [organization/public/v1/organization_api.proto](#organization_public_v1_organization_api-proto)
    - [GetOrganizationRequest](#organization-public-v1-GetOrganizationRequest)
    - [ListOrganizationsRequest](#organization-public-v1-ListOrganizationsRequest)
    - [ListOrganizationsResponse](#organization-public-v1-ListOrganizationsResponse)
  
    - [PublicOrganizationService](#organization-public-v1-PublicOrganizationService)
  
- [Scalar Value Types](#scalar-value-types)



<a name="organization_public_v1_organization-proto"></a>
<p align="right"><a href="#top">Top</a></p>

## organization/public/v1/organization.proto



<a name="organization-public-v1-PublicOrganization"></a>

### PublicOrganization
PublicOrganization は公開 Organization 表現。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| id | [string](#string) |  |  |
| schema_type | [string](#string) |  |  |
| name | [string](#string) |  |  |
| description | [string](#string) |  |  |
| image | [string](#string) |  |  |
| url | [string](#string) |  |  |





 

 

 

 



<a name="organization_public_v1_organization_api-proto"></a>
<p align="right"><a href="#top">Top</a></p>

## organization/public/v1/organization_api.proto



<a name="organization-public-v1-GetOrganizationRequest"></a>

### GetOrganizationRequest
GetOrganizationRequest は公開 Organization を取得する。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| name | [string](#string) |  | name は organizations/{id} 形式。 |






<a name="organization-public-v1-ListOrganizationsRequest"></a>

### ListOrganizationsRequest
ListOrganizationsRequest は公開 Organization 一覧を取得する。


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| page_size | [int32](#int32) |  |  |
| page_token | [string](#string) |  |  |






<a name="organization-public-v1-ListOrganizationsResponse"></a>

### ListOrganizationsResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| organizations | [PublicOrganization](#organization-public-v1-PublicOrganization) | repeated |  |
| next_page_token | [string](#string) |  |  |





 

 

 


<a name="organization-public-v1-PublicOrganizationService"></a>

### PublicOrganizationService
PublicOrganizationService は read-oriented な公開 Organization API。

| Method Name | Request Type | Response Type | Description |
| ----------- | ------------ | ------------- | ------------|
| GetOrganization | [GetOrganizationRequest](#organization-public-v1-GetOrganizationRequest) | [PublicOrganization](#organization-public-v1-PublicOrganization) |  |
| ListOrganizations | [ListOrganizationsRequest](#organization-public-v1-ListOrganizationsRequest) | [ListOrganizationsResponse](#organization-public-v1-ListOrganizationsResponse) |  |

 



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

