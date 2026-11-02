# ClipboardKit · 0.1.0

`Import clipboardkit` adds a single-use `ClipboardPayload` transaction above
Buoy's native `Clipboard`. The distinct package name avoids colliding with the
built-in Clipboard API. This package works on macOS, Windows and Linux through
Buoy's existing native clipboard implementation.

- `SetText(value)`, `SetPicture(picture)`, `SetFiles(files)` stage built-in,
  interoperable representations together.
- `SetData(mimeType, bytes)` stages an app-specific format, making a defensive
  byte copy. Repeating a type replaces its staged value.
- `SetJSON(mimeType, json)` serializes a structured app-specific representation.
- `Commit()` creates one native writer and commits all representations together.
  Empty payloads, repeat commits and editing an already-committed payload throw.
- `IsEmpty` and `IsCommitted` report transaction state.
- `CaptureClipboard(customTypes, includePicture = False)` captures known live
  text/files and optionally picture/custom types into a new payload. It is a
  best-effort multi-format read, not an atomic snapshot; unknown formats are
  neither enumerated nor preserved. Capturing does not write.

Custom types must be ASCII MIME `type/subtype` tokens without parameters.
Built-in text/image/file MIME collisions are rejected; use their dedicated setters.
On macOS, Buoy maps custom MIME strings into its own UTI namespace, so custom data
round-trips between Buoy apps but is not a general interchange format for arbitrary
other apps. Use Text/Picture/Files for normal cross-app interoperability.

Call `Commit()` only following a user Copy action. This library never watches,
clears, restores or commits the clipboard automatically. The native OS owns the
clipboard after commit; the package cannot promise OS-level acceptance feedback
because Buoy's `Clipboard.Close()` returns no status.
