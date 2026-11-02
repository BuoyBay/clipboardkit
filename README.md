# Multi-format clipboard payloads

`Import clipboardkit` adds a single-use `ClipboardPayload` transaction above
Buoy's native `Clipboard`. The distinct package name avoids colliding with the
built-in Clipboard API. This package works on macOS, Windows and Linux through
Buoy's existing native clipboard implementation.

Custom types must be ASCII MIME `type/subtype` tokens without parameters.
Built-in text/image/file MIME collisions are rejected; use their dedicated setters.
On macOS, Buoy maps custom MIME strings into its own UTI namespace, so custom data
round-trips between Buoy apps but is not a general interchange format for arbitrary
other apps. Use Text/Picture/Files for normal cross-app interoperability.

## Install

From a Buoy consumer project with BPM installed:

```sh
bpm add clipboardkit --git https://github.com/BuoyBay/clipboardkit.git --rev refs/heads/main
```

BPM records the resolved commit in its lockfile. Keep that lockfile with the
consumer project for reproducible installs.

## Example

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

## Build from source

With the native `build-packages` driver from [devtools](https://github.com/BuoyBay/devtools)
on your `PATH`, run from this checkout:

```sh
build-packages --root "$PWD" --compile-consumer clipboardkit
```

The driver checks source targets and compiles an import consumer. See the
[API guide](docs/API.md) for behavior, limits and any host prerequisites.

## Contributing

[Contributing](CONTRIBUTING.md) · [License](LICENSE)
