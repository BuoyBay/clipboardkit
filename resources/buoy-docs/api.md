---
title: "ClipboardKit API"
summary: "Stage text and structured representations in one explicit clipboard transaction."
category: "Reference"
order: 20
keywords: ["clipboardkit", "API", "lifecycle"]
symbols: ["ClipboardPayload", "ClipboardPayload.IsEmpty", "ClipboardPayload.IsCommitted", "ClipboardPayload.SetText", "ClipboardPayload.SetPicture", "ClipboardPayload.SetFiles", "ClipboardPayload.SetData", "ClipboardPayload.SetJSON", "ClipboardPayload.Commit", "CaptureClipboard"]
related: ["index.md", "getting-started.md", "typed-api.md"]
---

# ClipboardKit API

Import the `clipboardkit` package. Constructors below use the class name; invoke them with `New`. Listed members are public client APIs; native declarations and trampoline helpers are implementation details.

## Public surface

| Symbol | Contract |
| --- | --- |
| `ClipboardPayload` | Inert, initially empty staging object. |
| `ClipboardPayload.IsEmpty As Boolean` | True until a representation has been staged. |
| `ClipboardPayload.IsCommitted As Boolean` | True after the native writer has been closed by Commit. |
| `ClipboardPayload.SetText(value As String)` | Stages a text representation; an empty string is still a representation. |
| `ClipboardPayload.SetPicture(value As Picture)` | Stages a non-Nil native picture. |
| `ClipboardPayload.SetFiles(values As Array Of FileSystemItem)` | Copies the nonempty file-item array into staging. |
| `ClipboardPayload.SetData(mimeType As String, value As Bytes)` | Defensively copies custom bytes and replaces an existing staged value of the same normalized type. |
| `ClipboardPayload.SetJSON(mimeType As String, value As JSONItem)` | Serializes JSON to UTF-8 custom data. |
| `ClipboardPayload.Commit()` | Writes all staged representations through one native writer; single use. |
| `CaptureClipboard(customTypes As Array Of String, includePicture As Boolean = False) As ClipboardPayload` | Best-effort read of text/files plus requested custom types and optional picture. Unknown formats are not enumerated. |

## Ownership and timing

Setters stage data without touching the live clipboard. Call Commit from a deliberate user Copy action. After commit the payload is immutable and cannot be committed again. CaptureClipboard reads known representations into a new payload but does not commit or restore them.

## Errors and result interpretation

Empty commits and edits after commit throw InvalidArgumentException. Pictures and byte data must not be Nil; file lists must be nonempty and contain no Nil items. Custom MIME strings must be ASCII type/subtype tokens without parameters and must not collide with built-in text, PNG, or file types. Buoy Clipboard.Close returns no OS acceptance status.

## Platform behavior

The package uses Buoy native clipboard support on macOS, Windows, and Linux. On macOS custom MIME formats are mapped into Buoy-specific UTI names; use the dedicated text, picture, and file representations for normal interchange with other applications.

See the [complete usage example](getting-started.md) and the [package overview](index.md).

[Full typed API: properties, parameters, defaults, and returns](typed-api.md)
