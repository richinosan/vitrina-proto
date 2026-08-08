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
  
- [event/v1/api.proto](#event_v1_api-proto)
    - [EventService](#event-v1-EventService)
  
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
| organizer_json | [string](#string) |  |  |
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
| organizer_json | [string](#string) |  |  |





 

 

 

 



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

