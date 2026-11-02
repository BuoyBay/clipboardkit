---
title: "ClipboardKit getting started"
summary: "Install clipboardkit and use its core API with explicit application ownership."
category: "Guides"
order: 10
keywords: ["clipboardkit", "installation", "example"]
related: ["index.md", "api.md", "typed-api.md"]
---

# ClipboardKit getting started

## Install and import

Copy the sealed `clipboardkit-0.1.0.buipkg` archive into your project `packages/` directory, or install a source/registry dependency named `clipboardkit` using BPM and sync it. Then use `Import clipboardkit`. The archive includes this documentation as package resources.

Use a consuming source filename such as `main.bui`; a local module named exactly like the package shadows its import.

## Complete usage example

The example is compiler-checked as a complete Buoy module. Functions and Subs are intended to be called from the consuming app at the appropriate user action or lifecycle event.

```basic
Import clipboardkit

Sub CopyGreeting()
    Dim payload As New ClipboardPayload()
    payload.SetText("Hello from Buoy")
    Dim details As JSONItem = Json.Parse("{\"kind\":\"greeting\"}")
    payload.SetJSON("application/x-buoy-greeting", details)
    payload.Commit()
End Sub
```

## Integrate with the application

Setters stage data without touching the live clipboard. Call Commit from a deliberate user Copy action. After commit the payload is immutable and cannot be committed again. CaptureClipboard reads known representations into a new payload but does not commit or restore them.

## Handle failures and unsupported targets

Empty commits and edits after commit throw InvalidArgumentException. Pictures and byte data must not be Nil; file lists must be nonempty and contain no Nil items. Custom MIME strings must be ASCII type/subtype tokens without parameters and must not collide with built-in text, PNG, or file types. Buoy Clipboard.Close returns no OS acceptance status.

The package uses Buoy native clipboard support on macOS, Windows, and Linux. On macOS custom MIME formats are mapped into Buoy-specific UTI names; use the dedicated text, picture, and file representations for normal interchange with other applications.

Return to the [overview](index.md) or consult the [API reference](api.md).
