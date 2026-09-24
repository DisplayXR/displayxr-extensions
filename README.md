# DisplayXR Extensions

OpenXR extension headers for 3D-display runtimes. **Auto-published** from [`displayxr-runtime`](https://github.com/DisplayXR/displayxr-runtime).

16 extensions, in 6 groups: what the runtime tells apps about the display, how an app drives the view math and 2D/3D compositing, how it hands the runtime its native window, the surface a swappable workspace controller uses, the app-agent bridge, and frame capture.

`Spec` links the formal specification where one is written; a dash means the header is the specification for now.

## Display capability

What the runtime tells apps about the 3D display they are rendering on.

| Extension | Header | Ver | Spec | Description |
|---|---|:--:|:--:|---|
| `XR_DXR_display_info` | [`XR_DXR_display_info.h`](include/openxr/XR_DXR_display_info.h) | 21 | [spec](https://github.com/DisplayXR/displayxr-runtime/blob/main/docs/specs/extensions/XR_DXR_display_info.md) | Display dimensions, eye-tracking modes, and the data needed for asymmetric (Kooima) projection |

## Rendering, projection & compositing

How an app drives the runtime's view math, declares which regions of its window are 3D, and hands pre-weave content to the vendor display processor — instead of re-implementing projection or weaving itself.

| Extension | Header | Ver | Spec | Description |
|---|---|:--:|:--:|---|
| `XR_DXR_depth_budget` | [`XR_DXR_depth_budget.h`](include/openxr/XR_DXR_depth_budget.h) | 4 | [spec](https://github.com/DisplayXR/displayxr-runtime/blob/main/docs/specs/extensions/XR_DXR_depth_budget.md) | Advisory limit on how far behind the display plane a transparent app may render, chained on XrViewState at xrLocateViews |
| `XR_DXR_display_zones` | [`XR_DXR_display_zones.h`](include/openxr/XR_DXR_display_zones.h) | 3 | [spec](https://github.com/DisplayXR/displayxr-runtime/blob/main/docs/specs/extensions/XR_DXR_display_zones.md) | A layout of independent 3D zones and flat 2D zones across one display, each 3D zone with its own view rig, plus the wish mask a switchable-lens panel honours; poll xrGetDisplayZoneRecommendedViewSizeDXR for per-zone sizes — XrEventDataDisplayZoneMetricsChangedDXR is deprecated and never emitted |
| `XR_DXR_local_3d_zone` | [`XR_DXR_local_3d_zone.h`](include/openxr/XR_DXR_local_3d_zone.h) | 5 | — | Per-pixel 3D-ness mask over an app's own window, with the flat 2D side as a first-class post-weave composition layer; its view-size event is soft-deprecated since spec 5 in favour of the Khronos XR_EXT_view_configuration_views_change, but still emitted unchanged |
| `XR_DXR_view_rig` | [`XR_DXR_view_rig.h`](include/openxr/XR_DXR_view_rig.h) | 3 | — | App declares a display or camera rig descriptor and consumes render-ready XrView{pose, fov}; the runtime owns the projection math |
| `XR_DXR_weave` | [`XR_DXR_weave.h`](include/openxr/XR_DXR_weave.h) | 11 | [spec](https://github.com/DisplayXR/displayxr-runtime/blob/main/docs/specs/extensions/XR_DXR_weave.md) | Window-bound synchronous weave for present-owners: hand the runtime a stereo texture and a window rect, get back a weaved shared texture and a fence |

## App window binding

How an app hands its native window to the runtime so the compositor can output into it.

| Extension | Header | Ver | Spec | Description |
|---|---|:--:|:--:|---|
| `XR_DXR_android_surface_binding` | [`XR_DXR_android_surface_binding.h`](include/openxr/XR_DXR_android_surface_binding.h) | 2 | [spec](https://github.com/DisplayXR/displayxr-runtime/blob/main/docs/specs/extensions/XR_DXR_android_surface_binding.md) | App-provided Android Surface / ANativeWindow, republished across background and resume, with the per-frame window rect |
| `XR_DXR_cocoa_window_binding` | [`XR_DXR_cocoa_window_binding.h`](include/openxr/XR_DXR_cocoa_window_binding.h) | 6 | [spec](https://github.com/DisplayXR/displayxr-runtime/blob/main/docs/specs/extensions/XR_DXR_cocoa_window_binding.md) | App-provided NSView, IOSurface sharing |
| `XR_DXR_macos_gl_binding` | [`XR_DXR_macos_gl_binding.h`](include/openxr/XR_DXR_macos_gl_binding.h) | 2 | — | macOS OpenGL graphics binding |
| `XR_DXR_wayland_surface_binding` | [`XR_DXR_wayland_surface_binding.h`](include/openxr/XR_DXR_wayland_surface_binding.h) | 2 | [spec](https://github.com/DisplayXR/displayxr-runtime/blob/main/docs/specs/extensions/XR_DXR_wayland_surface_binding.md) | App-provided wl_display and wl_surface (desktop Linux), plus the app-declared surface size that makes windowed Wayland work |
| `XR_DXR_win32_window_binding` | [`XR_DXR_win32_window_binding.h`](include/openxr/XR_DXR_win32_window_binding.h) | 8 | [spec](https://github.com/DisplayXR/displayxr-runtime/blob/main/docs/specs/extensions/XR_DXR_win32_window_binding.md) | App-provided HWND, shared texture, canvas sub-rect |
| `XR_DXR_xlib_window_binding` | [`XR_DXR_xlib_window_binding.h`](include/openxr/XR_DXR_xlib_window_binding.h) | 2 | [spec](https://github.com/DisplayXR/displayxr-runtime/blob/main/docs/specs/extensions/XR_DXR_xlib_window_binding.md) | App-provided X11 Display* and Window (desktop Linux) |

## Workspace controller surface

The contract that lets a workspace controller — the DisplayXR Shell, or any third-party / OEM / vertical / AI-agent equivalent — drive the spatial-desktop layer on top of the runtime. Activation is gated by orchestrator-PID match; the runtime trusts whatever binary it was configured to spawn.

| Extension | Header | Ver | Spec | Description |
|---|---|:--:|:--:|---|
| `XR_DXR_spatial_workspace` | [`XR_DXR_spatial_workspace.h`](include/openxr/XR_DXR_spatial_workspace.h) | 24 | [spec](https://github.com/DisplayXR/displayxr-runtime/blob/main/docs/specs/extensions/XR_DXR_spatial_workspace.md) | Multi-app composition: window pose, hit-test, capture, overlay, modal input grab |
| `XR_DXR_workspace_file_dialog` | [`XR_DXR_workspace_file_dialog.h`](include/openxr/XR_DXR_workspace_file_dialog.h) | 1 | [spec](https://github.com/DisplayXR/displayxr-runtime/blob/main/docs/specs/extensions/XR_DXR_workspace_file_dialog.md) | Async spatial-native file picker spawned by the active workspace controller, with fallback to the platform dialog |

## Agent control

How applications plug into the AI-agent surface, exposing their own actions through the same MCP framework the runtime and workspace controllers use.

| Extension | Header | Ver | Spec | Description |
|---|---|:--:|:--:|---|
| `XR_DXR_mcp_tools` | [`XR_DXR_mcp_tools.h`](include/openxr/XR_DXR_mcp_tools.h) | 1 | [spec](https://github.com/DisplayXR/displayxr-runtime/blob/main/docs/specs/extensions/XR_DXR_mcp_tools.md) | An app registers its own MCP tools with the runtime's agent surface; calls arrive on the OpenXR event queue |

## Capture

Getting the composed multi-view frame back out of the runtime — for screenshots, recording, and dataset generation.

| Extension | Header | Ver | Spec | Description |
|---|---|:--:|:--:|---|
| `XR_DXR_atlas_capture` | [`XR_DXR_atlas_capture.h`](include/openxr/XR_DXR_atlas_capture.h) | 3 | — | Vendor-neutral PNG snapshot of the multi-view atlas at a caller-selected compositor stage, for any app class |

## Usage

Copy the headers into your project's OpenXR include path, or add this repo as a submodule:

```bash
git submodule add https://github.com/DisplayXR/displayxr-extensions.git external/displayxr-extensions
# Then add external/displayxr-extensions/include to your include path
```

`extensions.json` at the repo root is the same table, machine-readable — name, group, title, summary, `specVersion`, header path and spec URL — for tooling that wants the set without parsing headers.

## Full Documentation

- [Extension Specs](https://github.com/DisplayXR/displayxr-runtime/tree/main/docs/specs/extensions) — formal specifications with examples
- [Getting Started](https://github.com/DisplayXR/displayxr-runtime/tree/main/docs/getting-started) — build and integrate with DisplayXR
- [displayxr-runtime](https://github.com/DisplayXR/displayxr-runtime) — the OpenXR runtime

## Provisional naming

`DXR` is DisplayXR's Khronos-registered OpenXR author ID. The `XR_DXR_*` extensions themselves are **provisional** — they are not yet registered in the Khronos OpenXR registry: extension numbers and `XrStructureType` values sit in a provisional experimental block (`1004999xxx`) pending official assignment. Extension names are expected to be stable; numeric values are not. (These extensions previously shipped under provisional `XR_EXT_*` names; the rename did not restart `SPEC_VERSION` — the interface history continues.) See [GOVERNANCE.md](GOVERNANCE.md).

## License

[Apache-2.0](LICENSE). These headers are original, DisplayXR-authored extension definitions — the same license the Khronos OpenXR headers use, chosen for its explicit patent grant on the path to Khronos ratification. The per-file `SPDX-License-Identifier` is authoritative.

## Auto-Published

Headers, this README and `extensions.json` are all generated from `displayxr-runtime` on every push to its main — the header set from `src/external/openxr_includes/openxr/XR_DXR_*.h`, the per-extension notes from `docs/specs/extensions/index.json`, by `scripts/gen_extensions_index.py`. Do not edit them here — changes will be overwritten. Open PRs against the runtime; a header whose note is missing fails that repo's `lint` workflow, which is why this table cannot fall behind the headers again.
