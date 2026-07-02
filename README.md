# DisplayXR Extensions

OpenXR extension headers for 3D-display runtimes. **Auto-published** from [`displayxr-runtime`](https://github.com/DisplayXR/displayxr-runtime).

The headers fall into three groups: what the runtime tells apps about the display, how an app gives the runtime its native window, and the surface a swappable workspace controller uses to drive multi-app composition.

## Display capability

| Header | Extension | Description |
|--------|-----------|-------------|
| [`XR_EXT_display_info.h`](include/openxr/XR_EXT_display_info.h) | `XR_EXT_display_info` | Display dimensions, eye-tracking modes, and the data needed for asymmetric (Kooima) projection |

## App window binding

| Header | Extension | Description |
|--------|-----------|-------------|
| [`XR_EXT_win32_window_binding.h`](include/openxr/XR_EXT_win32_window_binding.h) | `XR_EXT_win32_window_binding` | App-provided HWND, shared texture, canvas sub-rect |
| [`XR_EXT_cocoa_window_binding.h`](include/openxr/XR_EXT_cocoa_window_binding.h) | `XR_EXT_cocoa_window_binding` | App-provided NSView, IOSurface sharing |
| [`XR_EXT_macos_gl_binding.h`](include/openxr/XR_EXT_macos_gl_binding.h) | `XR_EXT_macos_gl_binding` | macOS OpenGL graphics binding |

## Workspace controller surface

The contract that lets a workspace controller — the [DisplayXR Shell](https://github.com/DisplayXR/displayxr-shell-releases), or any third-party / OEM / vertical / AI-agent equivalent — drive the spatial-desktop layer on top of the runtime. Activation is gated by orchestrator-PID match; the runtime trusts whatever binary it was configured to spawn.

| Header | Extension | Description |
|--------|-----------|-------------|
| [`XR_EXT_spatial_workspace.h`](include/openxr/XR_EXT_spatial_workspace.h) | `XR_EXT_spatial_workspace` | Multi-app composition: window pose, hit-test, capture, overlay, modal input grab |

## Usage

Copy the headers into your project's OpenXR include path, or add this repo as a submodule:

```bash
git submodule add https://github.com/DisplayXR/displayxr-extensions.git external/displayxr-extensions
# Then add external/displayxr-extensions/include to your include path
```

## Full Documentation

- [Extension Specs](https://github.com/DisplayXR/displayxr-runtime/tree/main/docs/specs) — formal specifications with examples
- [Getting Started](https://github.com/DisplayXR/displayxr-runtime/tree/main/docs/getting-started) — build and integrate with DisplayXR
- [displayxr-runtime](https://github.com/DisplayXR/displayxr-runtime) — the OpenXR runtime

## Provisional naming

The `XR_EXT_*` identifiers are **provisional** — they are not registered in the Khronos OpenXR registry. They are placeholders used during DisplayXR incubation and will be re-registered (and may be renamed to a registered `XR_<AUTHORID>_` prefix) through the official Khronos process on the EXT → KHR path. Do not treat the names or numeric values as stable. See [GOVERNANCE.md](GOVERNANCE.md).

## License

[Apache-2.0](LICENSE). These headers are original, DisplayXR-authored extension definitions — the same license the Khronos OpenXR headers use, chosen for its explicit patent grant on the path to Khronos ratification. The per-file `SPDX-License-Identifier` is authoritative.

## Auto-Published

These headers are automatically synced from `displayxr-runtime/src/external/openxr_includes/openxr/XR_EXT_*.h` on every push to main. Do not edit directly — changes will be overwritten.
