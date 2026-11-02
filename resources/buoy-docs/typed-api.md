---
title: "clipboardkit typed API"
summary: "Source-derived public signatures, properties, parameters, defaults, and return values."
category: "Reference"
order: 21
types: ["ClipboardPayload"]
dependencies: []
symbols: ["ClipboardPayload"]
related: ["api.md", "getting-started.md", "index.md"]
---

# clipboardkit typed API

Generated from the package source declarations. Platform guards are shown where present; inherited members are documented on the base type. See the [API contracts](api.md) for behavior and limitations.

## ClipboardPayload

`Public Class ClipboardPayload`

A single-use, multi-representation clipboard transaction. Nothing is written until Commit.

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `IsCommitted` | `Boolean` | Yes | No | — | — |
| `IsEmpty` | `Boolean` | Yes | No | — | — |

### SetText

`Public Sub SetText(value As String)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `value` | `String` | `ByVal` | Required |

Returns: no value.

### SetPicture

`Public Sub SetPicture(value As Picture)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `value` | `Picture` | `ByVal` | Required |

Returns: no value.

### SetFiles

`Public Sub SetFiles(values As Array Of FileSystemItem)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `values` | `Array Of FileSystemItem` | `ByVal` | Required |

Returns: no value.

### SetData

`Public Sub SetData(mimeType As String, value As Bytes)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `mimeType` | `String` | `ByVal` | Required |
| `value` | `Bytes` | `ByVal` | Required |

Returns: no value.

### SetJSON

`Public Sub SetJSON(mimeType As String, value As JSONItem)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `mimeType` | `String` | `ByVal` | Required |
| `value` | `JSONItem` | `ByVal` | Required |

Returns: no value.

### Commit

`Public Sub Commit()`

No parameters.

Returns: no value.

### CaptureClipboard

`Public Function CaptureClipboard(customTypes As Array Of String, includePicture As Boolean = False) As ClipboardPayload`

Best-effort capture of known representations; unknown clipboard formats are not enumerated.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `customTypes` | `Array Of String` | `ByVal` | Required |
| `includePicture` | `Boolean` | `ByVal` | `False` |

#### Returns

| Type |
| --- |
| `ClipboardPayload` |
