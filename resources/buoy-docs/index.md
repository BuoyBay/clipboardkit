---
title: "ClipboardKit"
summary: "Stage text and structured representations in one explicit clipboard transaction."
category: "Overview"
order: 0
keywords: ["clipboardkit"]
related: ["getting-started.md", "api.md", "typed-api.md"]
---

# ClipboardKit

ClipboardPayload groups interoperable text, pictures, files, and app-specific MIME data into a single-use transaction. It builds on Buoy Clipboard and avoids a package-name collision with that built-in API.

## Platform support

The package uses Buoy native clipboard support on macOS, Windows, and Linux. On macOS custom MIME formats are mapped into Buoy-specific UTI names; use the dedicated text, picture, and file representations for normal interchange with other applications.

## Start reading

- [Getting started](getting-started.md) walks through installation and a complete example.
- [API reference](api.md) describes public symbols, state, errors, and ownership.

## Scope

Setters stage data without touching the live clipboard. Call Commit from a deliberate user Copy action. After commit the payload is immutable and cannot be committed again. CaptureClipboard reads known representations into a new payload but does not commit or restore them.
