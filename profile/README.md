<table width="100%">
<tr>
<td width="180" valign="middle" align="center">

<img src="https://raw.githubusercontent.com/ARKlight-Ecosystem/ARKlight/alpha/ARKlight-logo.png" alt="ARKlight" width="160" height="160">

</td>
<td valign="middle">
<div align="center">

# ARKlight Ecosystem

**Write Python. Ship plain dependency free Websi9.**

**A Python-first compiler for building static websites where developers work
with a structured component API, while the output remains ordinary, dependency-free `Hyper Text Markup Language` `Casscading Style Sheets` `JavaScript`. and the tools that grow around it.**

</div>
</td>
</tr>
</table>

---

## What is ARKlight?

ARKlight lets you describe a website in Python and compiles it to standard, dependency-free
HTML, CSS, and JavaScript. **The browser never executes Python.**

```python
# include <stdlib.ARKlight>

site = Site()

@site.page("/")
def home():
    return Page(
        Heading("ARKlight"),
        Text("Build websites with Python."),
        Button("Get Started"),
    )
```

```bash
arklight build site.py.         # writes ARK/index.html
arklight pack ARK -o site.ark   # one portable .ark bundle
```

## Repositories

| Repository | What it is | License |
|---|---|---|
| [**ARKlight**](https://github.com/ARKlight-Ecosystem/ARKlight) | The Python compiler and CLI: source → AST → validated, backend-independent IR → HTML / CSS / JS backends. Where sites are authored and where the language evolves. | GPL-3.0-or-later |
| [**C_ARKlight**](https://github.com/ARKlight-Ecosystem/C_ARKlight) | The compiler core in C (`libcarklight`): a small, dependency-free library behind a stable ABI that builds sites from the `.arklight` encoding of the IR. Work in progress. | GPL-3.0-or-later |
| [**ARKlight Viewer for Android**](https://github.com/ARKlight-Ecosystem/ARKlight-Viewer-for-Android-Devices) | Tap a `.ark` bundle and browse the whole multi-page site offline, with no server. Sealed and passphrase-protected bundles supported. Android 7.0+. | Apache-2.0 |
| [**ARKlight Component Collections**](https://github.com/ARKlight-Ecosystem/ARKlight-Component-Collections) | ACC: the planned package and distribution system for ARKlight components, actions, styles, and other extensions. Early design stage. | Apache-2.0 |
| [**ARKlight Ecosystem**](https://github.com/ARKlight-Ecosystem) | This repos purpose is centralised Documentation and getting Poll requests if a user has any feature requests or suggestions that respects ARKlight's philosophy `Compiler First - Runtime Last` It's recommended to drop a docs here | None |

## How the pieces fit

```text
Python source
   │
   ▼
ARKlight (Python) ── AST → IR → HTML / CSS / JS ──▶ static site ──▶ .ark bundle
   │                                                                     │
   │ .arklight (encoded IR)                                              ▼
   ▼                                                              ARKlight Viewer
C_ARKlight: the same outputs, built in                                (Android)
dependency-free C behind a stable ABI

ACC: extension packages that plug into ARKlight
```

## Design principles

- **Intent, not markup.** The IR models what a site *means*; HTML is just one backend's
  rendering of it, so CSS, JS, and future targets all run over the same tree.
- **Static output.** What ships is plain files. No runtime, no framework, no server required.
- **Fast frontier, slow core.** ARKlight in Python moves quickly and defines what's next. The
  C core deliberately trails it, picking up only what has shipped and stayed stable.

## Status 

```text 
As of when this Readme was done
```

Early and moving fast. ARKlight is at `0.54.0` (main) and ARKlight (Alpha) is at `0.0651`, with new work developed on the
`alpha` branch. C_ARKlight tracks an earlier, frozen ARKlight release by design. The Android
viewer builds APKs in CI, and ACC is still on the drawing board.

## Try it

```bash
git clone https://github.com/ARKlight-Ecosystem/ARKlight.git
cd ARKlight
pip install -e .                              # Python 3.10+
arklight build examples/hello_site/site.py
```

More in the [ARKlight README](https://github.com/ARKlight-Ecosystem/ARKlight#readme).
More in the [ARKlight Ecosystem](https://github.com/ARKlight-Ecosystem/Docs) 
