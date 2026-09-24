# ARKlight Ecosystem Documentation

The central documentation index for the ARKlight ecosystem. It **links** to the docs; it
does not move or copy them. Every document stays in the repository that owns it, and this
page is the one place that maps them all.

> **Verified against:** ARKlight `alpha` @ `10fa1b2` (2026-09-24) and `main` @ `4e684183`
> (2026-09-24); C_ARKlight @ `a87a9ba`; ARKlight Component Collections @ `c8dcbb4`;
> ARKlight Viewer @ `5acab6f`.
> ARKlight links point at the **`alpha`** branch, where the docs and the language are
> developed. `main` catches up in releases and is older.

## Start here

1. [**The Pitch**](https://github.com/ARKlight-Ecosystem/ARKlight/blob/alpha/docs/Foundational/PITCH.md):
   the problem ARKlight is solving and the larger idea behind it.
2. [**What is ARKlight?**](https://github.com/ARKlight-Ecosystem/ARKlight/blob/alpha/docs/Foundational/WHAT-ARKLIGHT-IS.md):
   a concise definition of what it is, how it works, and what it provides today.
3. [**Foundational docs**](https://github.com/ARKlight-Ecosystem/ARKlight/tree/alpha/docs/Foundational):
   architecture, compiler model, and design decisions, indexed below.

## Philosophy

- **"The browser never executes Python."** Output is plain HTML, CSS, and vanilla JS; the
  compiler is the only thing that runs Python
  ([`arklight/__init__.py`](https://github.com/ARKlight-Ecosystem/ARKlight/blob/alpha/arklight/__init__.py)).
- **"No eval, no new Function, no string ever executed as code."** The shipped runtime never
  turns a string into executable code, even through a vendored dependency's optional feature
  ([`js/render.py`](https://github.com/ARKlight-Ecosystem/ARKlight/blob/alpha/arklight/backend/js/render.py),
  [`html/attrs.py`](https://github.com/ARKlight-Ecosystem/ARKlight/blob/alpha/arklight/backend/html/attrs.py)).
- **"Fail loudly at build time, not silently in the browser."** Anything wrong with a site
  should raise a `ValidationError` during `arklight build`, never surface as broken behavior
  after deployment
  ([`ir/validate.py`](https://github.com/ARKlight-Ecosystem/ARKlight/blob/alpha/arklight/ir/validate.py),
  [`config.py`](https://github.com/ARKlight-Ecosystem/ARKlight/blob/alpha/arklight/config.py)).
- **"Only ship what's used."** The compiler emits the minimum HTML, CSS, and JS a site's IR
  actually needs; nothing is bundled unconditionally
  ([`js/htmx.py`](https://github.com/ARKlight-Ecosystem/ARKlight/blob/alpha/arklight/backend/js/htmx.py)).
- **Compiled markup is honest about what it does.** "Inspectable, predictable" output is the
  point of compiling to plain HTML at all.
- **Compiler first, runtime last.** The compiler owns the work; the target runtime gets as
  little as possible. The full agreement, including the four-question rule for judging any
  new feature, is in
  [`SYSTEM-DESIGN-AGREEMENTS.md`](https://github.com/ARKlight-Ecosystem/ARKlight/blob/alpha/docs/Foundational/SYSTEM-DESIGN-AGREEMENTS.md).

## Documentation by repository

| Repository | Where its docs are |
|---|---|
| [**ARKlight**](https://github.com/ARKlight-Ecosystem/ARKlight) | [`docs/README.md`](https://github.com/ARKlight-Ecosystem/ARKlight/blob/alpha/docs/README.md) (on `alpha`), detailed [below](#arklight-docs) |
| [**C_ARKlight**](https://github.com/ARKlight-Ecosystem/C_ARKlight) | [`docs/`](https://github.com/ARKlight-Ecosystem/C_ARKlight/tree/main/docs), detailed [below](#c_arklight-docs) |
| [**ARKlight Component Collections**](https://github.com/ARKlight-Ecosystem/ARKlight-Component-Collections) | [`docs/README.md`](https://github.com/ARKlight-Ecosystem/ARKlight-Component-Collections/blob/main/docs/README.md) |
| [**ARKlight Viewer for Android**](https://github.com/ARKlight-Ecosystem/ARKlight-Viewer-for-Android-Devices) | [`ARCHITECTURE.md`](https://github.com/ARKlight-Ecosystem/ARKlight-Viewer-for-Android-Devices/blob/main/ARCHITECTURE.md) |

---

## ARKlight docs

Each ARKlight docs folder is one *state* in a lifecycle, not a topic. A doc moves from one
folder to the next as a decision is made:

| State | Folder | Leaves the folder when |
|---|---|---|
| Speculative, not proposed as work | [`Far Future Concern/`](https://github.com/ARKlight-Ecosystem/ARKlight/tree/alpha/docs/Far%20Future%20Concern) | Picked up for real: graduates to `Backends/` or `Proposals/`. |
| Proposed, not yet decided | [`Proposals/`](https://github.com/ARKlight-Ecosystem/ARKlight/tree/alpha/docs/Proposals) | Accepted (moves to `Implementation/`) or rejected (removed). |
| Accepted, staged, in flight | [`Implementation/`](https://github.com/ARKlight-Ecosystem/ARKlight/tree/alpha/docs/Implementation), or [`Backends/`](https://github.com/ARKlight-Ecosystem/ARKlight/tree/alpha/docs/Backends) for a specific backend | Every stage ships: the outcome is captured in version history and the changelog. |
| Shipped, user-facing summary | [`version history/`](https://github.com/ARKlight-Ecosystem/ARKlight/tree/alpha/docs/version%20history) | Never. One file per shipped version. |
| Shipped, permanent design rationale | [`Foundational/`](https://github.com/ARKlight-Ecosystem/ARKlight/tree/alpha/docs/Foundational) | Never. Updated in place. |

The `new js backend proposal/` folder that used to sit alongside these is gone: the
vdom-vs-none decision was made (vdom, vendoring a bare `snabbdom` core), shipped as
`v0.054`, and its rationale now lives permanently in
[`Foundational/DESIGN-NOTES.md`](https://github.com/ARKlight-Ecosystem/ARKlight/blob/alpha/docs/Foundational/DESIGN-NOTES.md).

### Foundational (permanent)

These files never leave their folder, so they are indexed file by file. Each folder's own
README is the complete list.
[Folder README](https://github.com/ARKlight-Ecosystem/ARKlight/blob/alpha/docs/Foundational/README.md).

| File | Covers |
|---|---|
| [`WHAT-ARKLIGHT-IS.md`](https://github.com/ARKlight-Ecosystem/ARKlight/blob/alpha/docs/Foundational/WHAT-ARKLIGHT-IS.md) | The project's own definition, opening with "The Goal": framework-comparable developer experience while enforcing ARKlight's philosophy, for the Python and Education communities. |
| [`PITCH.md`](https://github.com/ARKlight-Ecosystem/ARKlight/blob/alpha/docs/Foundational/PITCH.md) | The conversational pitch: compiler-first/runtime-last, the closed component vocabulary, user-defined components, downstream packaging (PWAs, `.ark` bundles, Android, Linux desktop), and ACC. |
| [`V1-DEFINITION.md`](https://github.com/ARKlight-Ecosystem/ARKlight/blob/alpha/docs/Foundational/V1-DEFINITION.md) | What `v1.0 -- Stable compiler` means and where its scope ends: the web parts of the compiler only, not native backends, experimental features, or ACC. |
| [`ARCHITECTURE.md`](https://github.com/ARKlight-Ecosystem/ARKlight/blob/alpha/docs/Foundational/ARCHITECTURE.md) | High-level design: how source is parsed, compiled to IR, and rendered by a backend, plus the milestone table. |
| [`SYSTEM-DESIGN-AGREEMENTS.md`](https://github.com/ARKlight-Ecosystem/ARKlight/blob/alpha/docs/Foundational/SYSTEM-DESIGN-AGREEMENTS.md) | The "compiler first, runtime last" agreement: what the compiler owns vs. delegates, when it may specialize per target, and the four-question rule for new features. |
| [`GETTING-STARTED.md`](https://github.com/ARKlight-Ecosystem/ARKlight/blob/alpha/docs/Foundational/GETTING-STARTED.md) | Install (pip and the Debian/Ubuntu package), the annotated repository layout, and the `pytest` workflow. |
| [`AUTHORING-GUIDE.md`](https://github.com/ARKlight-Ecosystem/ARKlight/blob/alpha/docs/Foundational/AUTHORING-GUIDE.md) | The full public component, behavior, and state API reference. |
| [`CLI-REFERENCE.md`](https://github.com/ARKlight-Ecosystem/ARKlight/blob/alpha/docs/Foundational/CLI-REFERENCE.md) | Every shipped `arklight` subcommand, its flags, and worked examples. |
| [`CONFIGURABILITY.md`](https://github.com/ARKlight-Ecosystem/ARKlight/blob/alpha/docs/Foundational/CONFIGURABILITY.md) | The "reachability rule": which fixed internal values become a per-site kwarg or CLI flag, and which stay constants. |
| [`USER-DEFINED-COMPONENTS.md`](https://github.com/ARKlight-Ecosystem/ARKlight/blob/alpha/docs/Foundational/USER-DEFINED-COMPONENTS.md) | Reusable components: props, default styling, macro and registry modes, component-owned state, scope boundaries. |
| [`PLATFORM-APIS.md`](https://github.com/ARKlight-Ecosystem/ARKlight/blob/alpha/docs/Foundational/PLATFORM-APIS.md) | Settled design for the platform API layer (`PlatformAPI.notify`, `.clipboard_write`): compiler owns the interface, backends own the implementation, Web is the default. |
| [`ACC-CAPABILITIES.md`](https://github.com/ARKlight-Ecosystem/ARKlight/blob/alpha/docs/Foundational/ACC-CAPABILITIES.md) | The ACC capability-discovery hook in `arklight/capabilities.py`: the `arklight.capabilities` entry-point contract and diagnostics. |
| [`EXPERIMENTAL-APIS.md`](https://github.com/ARKlight-Ecosystem/ARKlight/blob/alpha/docs/Foundational/EXPERIMENTAL-APIS.md) | Unstable or opt-in APIs and their stability guarantees. |
| [`DESIGN-NOTES.md`](https://github.com/ARKlight-Ecosystem/ARKlight/blob/alpha/docs/Foundational/DESIGN-NOTES.md) | Rationale and trade-offs behind key design decisions. |
| [`DEPLOYMENT-CLI.md`](https://github.com/ARKlight-Ecosystem/ARKlight/blob/alpha/docs/Foundational/DEPLOYMENT-CLI.md) | **Design only, not implemented.** The planned `arklight deploy` subcommand. |

### Everything else in ARKlight docs

These folders change as work ships: files move, graduate, or get deleted. So this page
links to each folder's own README, which is the source of truth, instead of copying a
file list that would go stale.

| Folder | What's in it | Index |
|---|---|---|
| Backends | Staging plans for the Android and desktop packaging backends. The old Neutralino.js plan has been removed outright (not just superseded) in favor of a purpose-built native desktop host/packager | [README](https://github.com/ARKlight-Ecosystem/ARKlight/blob/alpha/docs/Backends/README.md) |
| Proposals | Design proposals awaiting a decision, or accepted and staged: JS vocabulary, URL state, providers, the `arklight assistant` CLI, project knowledge, runtime error handling, the Platform API IR, the Rei language, the AVM/WASM sandbox, KaiOS as a native target, and the alpha issue register, among others | [README](https://github.com/ARKlight-Ecosystem/ARKlight/blob/alpha/docs/Proposals/README.md) |
| Implementation | Rung-by-rung landing orders for accepted proposals | [README](https://github.com/ARKlight-Ecosystem/ARKlight/blob/alpha/docs/Implementation/README.md) |
| version history | The user-facing overview of each shipped `alpha` milestone | [README](https://github.com/ARKlight-Ecosystem/ARKlight/blob/alpha/docs/version%20history/README.md) |
| Far Future Concern | Speculative backlog: KaiOS, Windows Phone, and a not-yet-accepted, post-`v1.0` PocketBase-shaped data-service proposal | [README](https://github.com/ARKlight-Ecosystem/ARKlight/blob/alpha/docs/Far%20Future%20Concern/README.md) |
| reference | Vendored/reference material read for design purposes but not imported by any shipping code, e.g. a study copy of ELIZA behind the Rei compiler-narrator proposal | *(no folder README yet)* |

---

## C_ARKlight docs

The C compiler core (`libcarklight`). Status: work in progress. It tracks an earlier, frozen
ARKlight release by design.

| File | Covers |
|---|---|
| [`TERMINOLOGY.md`](https://github.com/ARKlight-Ecosystem/C_ARKlight/blob/main/docs/TERMINOLOGY.md) | Canonical: IR (the human-facing tree) vs. `.arklight` (its binary, machine-facing encoding). Read this first. |
| [`PROPOSAL.md`](https://github.com/ARKlight-Ecosystem/C_ARKlight/blob/main/docs/PROPOSAL.md) | The proposal and architecture: a C-ABI core carrying over only the stable subset of ARKlight. |
| [`ADDENDUM.md`](https://github.com/ARKlight-Ecosystem/C_ARKlight/blob/main/docs/ADDENDUM.md) | Revisions to the proposal: `.arklight`, the compile-time model, and modular-internal packaging. |
| [`IMPLEMENTATION.md`](https://github.com/ARKlight-Ecosystem/C_ARKlight/blob/main/docs/IMPLEMENTATION.md) | The staged plan for the C port, ordered so later stages never build on an unstable foundation. |
| [`ARKVM.md`](https://github.com/ARKlight-Ecosystem/C_ARKlight/blob/main/docs/ARKVM.md) | Design draft, not implemented: one name, two modes (`--minimal` / `--full`). |
| [`DESIGN-NOTES.md`](https://github.com/ARKlight-Ecosystem/C_ARKlight/blob/main/docs/DESIGN-NOTES.md) | Forward-looking notes on desktop and Android backends. Not a spec. |
| [`Think different, life easy/`](https://github.com/ARKlight-Ecosystem/C_ARKlight/tree/main/docs/Think%20different,%20life%20easy) | Quality system (TQM), allocation and disk I/O layer drafts, evolution-tracking notes, and a reference on how high-level language features compile to C. |

## ACC docs

[ARKlight Component Collections](https://github.com/ARKlight-Ecosystem/ARKlight-Component-Collections):
the planned package and distribution system for components, actions, styles, and other extensions.
[Docs index](https://github.com/ARKlight-Ecosystem/ARKlight-Component-Collections/blob/main/docs/README.md).

| File | Covers |
|---|---|
| [`acc-foundational-design.md`](https://github.com/ARKlight-Ecosystem/ARKlight-Component-Collections/blob/main/docs/design/acc-foundational-design.md) | What ACC is: the package and capability model, discovery via Python entry points, versioning, trust boundaries. |
| [`BUILD-TIME-ECOSYSTEM.md`](https://github.com/ARKlight-Ecosystem/ARKlight-Component-Collections/blob/main/docs/design/BUILD-TIME-ECOSYSTEM.md) | Why ACC sits beside the compiler rather than inside it. |
| [`IMPLEMENTATION-LADDER.md`](https://github.com/ARKlight-Ecosystem/ARKlight-Component-Collections/blob/main/docs/design/IMPLEMENTATION-LADDER.md) | The staged plan for ACC's first capability and component packages. |

## ARKlight Viewer docs

[`ARCHITECTURE.md`](https://github.com/ARKlight-Ecosystem/ARKlight-Viewer-for-Android-Devices/blob/main/ARCHITECTURE.md):
the implementation architecture of the Android app that opens `.ark` bundles as a native
file association.

---

## Suggest a feature

This repository accepts pull requests for feature requests and suggestions that respect
ARKlight's philosophy: **compiler first, runtime last**. Write your idea as a Markdown
document and open a pull request. Maintainers decide what is accepted.

A proposal is easiest to accept when it answers, in its own words:

- **What work does the compiler do, and what is left for the browser?** Read the
  [four-question rule](https://github.com/ARKlight-Ecosystem/ARKlight/blob/alpha/docs/Foundational/SYSTEM-DESIGN-AGREEMENTS.md)
  first.
- **How does a mistake fail?** Loudly at build time, not silently in the browser.
- **What does it add to the shipped output?** Only what a given site actually uses.
- **Does it ever execute a string as code?** It must not.

Accepted ideas follow the lifecycle above: proposed, then accepted and staged, then shipped.

## Keeping this index current

Each fact has one home. This page links; it does not copy. Foundational docs are listed
file by file because they never leave their folder. Every other folder is linked through
its own README, so a file that moves or is deleted only needs updating in one place.
When a link here breaks, fix the index in the same change that moved the doc.
