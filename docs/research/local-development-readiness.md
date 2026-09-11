# Local development readiness

Assessment of the Windows development machine and this Codex session on
11 September 2026. These are dated observations, not permanent environment
requirements. Recheck the relevant capability when provisioning a selected
toolchain or changing machines. This assessment does not select a game engine.

## What is established

There is no blanket restriction preventing Astra from downloading, installing
and running third-party libraries here. Two isolated installation probes passed
without administrator access. The harder dependencies are a suitable rendered
game loop, audio generation and observation, and any provider account access.

| Capability | Evidence and limit |
| --- | --- |
| Repository publication | Authenticated GitHub access worked: the README and related project documents were committed and pushed, with matching local and remote commit IDs. |
| Local command execution | PowerShell, Git, GitHub CLI, Node 22.19.0, npm 11.14.1, Python 3.13.14, uv 0.11.13, .NET SDK 9.0.318 and WinGet 1.29.290 were callable. |
| Node package installation | Installed and executed `picocolors@1.1.1` in an isolated directory under `scratch/`, with lifecycle scripts disabled. This proves an ordinary registry download and package import, not every native build or installer. |
| Python package installation | Created an isolated environment with uv, installed the binary wheel for `colorama==0.4.6`, and imported it successfully. No global Python environment was changed. |
| Native desktop observation and input | The installed Computer Use plugin launched Calculator, captured its rendered window, clicked a button and showed the resulting `7`. The temporary window was closed afterwards. Accessibility text was unavailable in this probe; screenshot-based input worked after window activation. Game-editor compatibility remains untested. |
| Browser graphics and input | A local HTTP page returned 200 in Node and isolated headless Edge 152.0.4191.66 through bundled Playwright 1.62.1. A click changed displayed state, and WebGL 2 rendered a rectangle with the expected pixel and no graphics error. The reported renderer was ANGLE / Intel Arc Pro Graphics / Direct3D 11, rather than a reported software renderer. This is not a game-performance benchmark. |
| Browser audio processing | An `AudioContext` was running at 48 kHz after a click, and offline rendering produced nonzero sine-wave samples. No sound was sent to physical output. Audible playback, loopback capture, recovery from a suspended context and musical quality remain untested. |
| Administrator access | The current process is not elevated. User-space packages work; an installer that actually requires Windows elevation may need the user. |

Probe files, downloads and explicitly configured temporary/cache locations were
confined to `scratch/capability-audit/`. They are disposable diagnostics, not
project dependencies or active work records.

## Hardware and installed software

The machine reports Windows 11 Pro x64, an Intel Core Ultra 9 185H processor
(16 cores, 22 logical processors), approximately 31.4 GiB usable RAM, and
approximately 744 GiB free on the system drive at the time of inspection.

`dxdiag` identifies Intel Arc Pro Graphics with 128 MB dedicated graphics
memory and approximately 18 GB shared memory, with DirectX feature levels
through 12_2. Shared memory should not be treated as equivalent to a discrete
GPU with that much dedicated VRAM. This supports investigating modest scenes;
it does not establish performance in any particular engine.

Unity, Unreal, Godot and Blender were not found through PATH, the Windows
uninstall inventory or their standard installation locations. This was not an
exhaustive search for portable copies. Visual Studio Community 2022 is present,
but the targeted `vswhere` query did not find the x86/x64 C++ toolchain component.

The [dependency options review](dependency-options.md) compares official engine
requirements, installation routes and music APIs. Its conclusions make a
browser toolchain and Godot useful first candidates to qualify on this machine.
Unity remains a candidate. Unreal warrants particular performance assessment
because the documented graphics-memory recommendation is not met here.

## Tools, MCPs, plugins and skills

| Facility | Current evidence and useful role |
| --- | --- |
| GitHub and Google Drive | GitHub publication and native Google Docs reads worked. Existing access is sufficient for the repository and source archive. |
| Context7 MCP | Library resolution and a query against Godot's official documentation returned results. This can supply version-relevant library documentation. |
| Browser automation | Connected browser tools are working, and a Playwright library is available in the bundled runtime. No new browser integration is yet a demonstrated prerequisite. |
| Windows Computer Use | The separate `node_repl` and `@oai/sky` route passed the native-app probe. The browser-only restriction of `cua_repl` does not describe this separate capability. |
| Image generation | An image-generation tool is exposed for creating or editing visual assets. It was not exercised during this assessment. |
| Engineering skills | The installed Matt Pocock skills include research, prototype, implementation, TDD, code review, diagnosis and handoff. Repository setup is already complete; no additional skill installation is required to start dependency qualification. |
| Engine-specific bridges | No Unity, Unreal or Godot MCP is currently configured in the local MCP inventory. Assess a bridge after choosing an engine if its CLI and existing UI tools leave a concrete control or observation gap. No third-party bridge has been selected or tested. |

Skills supply workflows; MCPs expose callable capabilities; plugins can bundle
both. Installing a skill does not establish an engine installation, a service
account or working credentials. New integrations may need authentication and
a server restart or new session before their tools are available.
[Official MCP documentation](https://learn.chatgpt.com/docs/extend/mcp),
[official plugin documentation](https://learn.chatgpt.com/docs/plugins).

## What may require the producer

- **An available Windows desktop for native UI work.** Computer Use uses the
  active foreground session. Keep it unlocked when native interaction is needed;
  concurrent use of the same mouse and keyboard can interfere. This restriction
  is distinct from ordinary shell or headless work.
  [Windows Computer Use](https://learn.chatgpt.com/docs/computer-use).
- **Account authentication and eligibility.** Sign-in, MFA and applicable
  account/licence decisions are conditional on the selected engine or service.
  There is no reason to create Unity or Epic accounts before selecting those
  routes.
- **A concrete paid API decision and secret provision.** The conventional
  OpenAI, Gemini/Google and ElevenLabs API-key environment variables were absent
  from this process. Other credential stores and account entitlements were not
  inspected. Select a provider and assess trial costs before provisioning its
  key securely. A ChatGPT/Codex plan does not fund third-party game API calls.
- **Actual elevation or app-access prompts.** Respond when a selected installer
  or app presents one. Ordinary package installation has already worked without
  elevation; no broad permissions change is indicated.
- **Musical judgement.** Automated timings, state checks, screenshots and audio
  measurements can support review. They do not establish that a song is funny,
  touching or worth hearing again; that remains part of the producer role.

## Remaining dependency qualification

Before gameplay implementation, qualify one candidate toolchain through a
rendered scene, player input, an observable state change, sound playback and
audio capture, then repeat after an edit. A successful headless build alone
does not establish that complete loop.

Separately, an agreed music-provider trial should measure delivery of an
event-specific sung contribution, delay to usable audio, intelligibility and
the transition back into the scene. API documentation does not establish these
results for this project. Provider candidates and their access requirements
are in the [dependency options review](dependency-options.md).
