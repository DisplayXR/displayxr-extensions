# DisplayXR Extensions

OpenXR extension headers for 3D display support. **Auto-published** from [`displayxr-runtime`](https://github.com/DisplayXR/displayxr-runtime).

## Headers

| Header | Extension | Description |
|--------|-----------|-------------|
| [`XR_EXT_display_info.h`](include/openxr/XR_EXT_display_info.h) | `XR_EXT_display_info` | Display dimensions, eye tracking, rendering modes |
| [`XR_EXT_win32_window_binding.h`](include/openxr/XR_EXT_win32_window_binding.h) | `XR_EXT_win32_window_binding` | App-provided HWND, shared texture, canvas sub-rect |
| [`XR_EXT_cocoa_window_binding.h`](include/openxr/XR_EXT_cocoa_window_binding.h) | `XR_EXT_cocoa_window_binding` | App-provided NSView, IOSurface sharing |
| [`XR_EXT_macos_gl_binding.h`](include/openxr/XR_EXT_macos_gl_binding.h) | `XR_EXT_macos_gl_binding` | macOS OpenGL graphics binding |

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

## Auto-Published

These headers are automatically synced from `displayxr-runtime/src/external/openxr_includes/openxr/XR_EXT_*.h` on every push to main. Do not edit directly — changes will be overwritten.
