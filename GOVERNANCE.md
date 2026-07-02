# DisplayXR Governance

DisplayXR is an **open incubator for spatial-display extensions to OpenXR**,
with the aim of upstreaming proven extensions into the official OpenXR
specification. This document describes how the project is governed during
incubation and the direction in which governance is intended to broaden as
adoption grows.

## Project status

DisplayXR is in its **incubation phase**, maintained by a small core team.
During this phase, vendor neutrality is enforced **by architecture and by
license**; governance is intended to broaden along the milestones described
below as more parties participate.

Neutrality in practice:

- The extension specifications, the runtime, the engine plugins, the MCP
  framework, and the demos are open source under permissive licenses (the
  runtime is a [Monado](https://monado.freedesktop.org/)-derived codebase
  under the Boost Software License 1.0).
- Every display vendor integrates through the same documented plug-in boundary
  ([ADR-019](https://github.com/DisplayXR/displayxr-runtime/blob/main/docs/adr/ADR-019-vendor-plugin-aux-boundary.md));
  no vendor has a privileged code path. The first such plug-in targets
  Leia-based displays — one implementation of that boundary among the many it
  is designed to support.
- All design work happens in public: extension specs, Architecture Decision
  Records, issues, and pull requests are open for review by anyone.

## Stewardship and conflict-of-interest disclosure

DisplayXR is currently stewarded by its founder and lead maintainer,
**David Fattal**. We state the resulting conflict directly rather than
leave it to be inferred: David Fattal is also an employee of **Leia Inc.**,
the display-technology vendor whose plug-in is the first integration of the
DisplayXR plug-in boundary.

Two commitments keep that overlap from translating into control of the neutral
core:

- **Leia holds no privileged position in the project.** No privileged code
  path — the runtime ships zero vendor identifiers, asserted in CI at the link
  level ([ADR-019](https://github.com/DisplayXR/displayxr-runtime/blob/main/docs/adr/ADR-019-vendor-plugin-aux-boundary.md));
  no privileged review authority; and **no reserved governance seat**. Leia
  integrates on exactly the same documented plug-in boundary as any other
  vendor, and `sim_display` proves the runtime runs with no vendor code at all.
- **Project identity is on a path to an independent steward.** As adoption
  grows, the project intends to move its identity — domain, GitHub
  organization, name, code-signing keys, and reference builds — to a small,
  independent light steward established outside any single vendor, and to
  institutionalize governance (a Technical Steering Committee, per the
  milestones below) once a second independent vendor adopts the plug-in
  boundary. Leia's standing role is founding-contributor recognition and a
  steering-committee seat on equal footing with other participants — not
  control over the standard or the reference implementation.

## How decisions are made (incubation phase)

- **Maintainers** review and merge changes. Final say on extension specs and
  runtime architecture rests with the project maintainers during incubation.
- **Design rationale is recorded publicly** as ADRs in the
  [runtime repo](https://github.com/DisplayXR/displayxr-runtime/tree/main/docs/adr).
  Architectural decisions take effect when they are written down.
- **Anyone can propose changes** via issues and pull requests on the relevant
  repository — no membership, fee, or affiliation required.

## Extension lifecycle

Modeled on the OpenXR working group's own process: a specification is not
accepted without a working implementation.

1. **Proposal** — open an issue or spec PR on
   [displayxr-extensions](https://github.com/DisplayXR/displayxr-extensions)
   describing the problem, the API surface, and which display classes it
   serves.
2. **Specification + reference implementation** — the spec PR must be
   accompanied by a working implementation in the DisplayXR runtime (or
   another conformant runtime). Spec and implementation are reviewed
   together.
3. **Experimental** — merged extensions ship in the runtime, marked
   experimental; the API may still change in response to real-world use.
4. **Stable** — once shipped applications depend on it and at least one full
   release cycle has passed without breaking changes, the extension is
   frozen per the project's versioning rules.
5. **Upstream** — extensions proven across multiple vendors' hardware are
   candidates for submission to the Khronos OpenXR registry.

### A note on extension naming

DisplayXR extensions use the `XR_EXT_*` prefix to reflect their design
intent: multi-vendor extensions, not vendor-specific ones. These identifiers
are **provisional** — they are not yet registered in the Khronos OpenXR
registry, and extensions that are upstreamed will be re-registered (and
possibly renamed) through the official Khronos process at that time.

## The path to shared governance

The transitions below describe the **direction the project intends to take**
as adoption grows. They are a statement of intent for how governance will
broaden, not binding commitments.

| Milestone | Intended governance change |
| --- | --- |
| **Today** — single-vendor incubation | Maintainer-led; all design in public. |
| **A second, independent display vendor adopts the plug-in boundary** | The project intends to form a Technical Steering Committee with representation from participating organizations alongside maintainer seats, and to move extension approval to that committee. |
| **Extensions in production use across multiple vendors' hardware** | The project intends to pursue formal Khronos engagement — an exploratory-group proposal and/or submission of proven extensions to the OpenXR working group. |
| **Khronos adoption** | DisplayXR's specs migrate to the official OpenXR registry; the project intends to continue as the open reference implementation and incubator for the next round of extensions. |

## How to participate

- **Display vendors** — implement the plug-in boundary for your hardware:
  see the [vendor guide](https://displayxr.org/vendors). A second independent
  plug-in is the milestone at which the project intends to move toward shared
  governance, as described above.
- **Engine and app developers** — build against the extensions, file issues
  where the API fights you. Real applications are what qualify an extension
  for upstreaming.
- **Contributors** — see [displayxr.org/contribute](https://displayxr.org/contribute)
  for the repo map, ADRs, and entry-point guides.

Questions about governance itself: open an issue on this repository.
