# DisplayXR Extensions

OpenXR extension specifications and headers for 3D displays.

## Extensions

| Extension | Description |
|-----------|-------------|
| `XR_EXT_display_info` | Display dimensions, eye tracking modes, view count |
| `XR_EXT_win32_window_binding` | App passes HWND to runtime (Windows) |
| `XR_EXT_cocoa_window_binding` | App passes NSWindow to runtime (macOS) |
| `XR_EXT_android_surface_binding` | App passes Surface to runtime (Android) |

## Status

Extraction planned during M4 milestone work (issues #3, #5, #8, #38 in the runtime repo). Headers currently live in `displayxr-runtime` under `src/external/openxr_includes/openxr/`.

## Related

- [displayxr-runtime](https://github.com/DisplayXR/displayxr-runtime) — Core OpenXR runtime
- [OpenXR Specification](https://registry.khronos.org/OpenXR/)
