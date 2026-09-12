# Local development readiness

Assessment of the Windows development machine and this Codex session on
11–12 September 2026. These are dated observations, not permanent environment
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
| Native desktop observation and input | The installed Computer Use plugin operated Calculator and Godot through rendered windows. Mouse and keyboard input changed the Godot scene; the editor imported and launched the project. Explicit window selection and activation were needed when another window obscured the editor. |
| Godot rendering, iteration and audio | The bounded [Godot qualification](#godot-qualification) passed rendering, native input, edit/rerun, clip playback, Master-bus recording, delayed phrase loading and cancellation checks. The producer confirmed that the live notes were audible, crisp, steady and unbroken. |
| Browser graphics and input | A local HTTP page returned 200 in Node and isolated headless Edge 152.0.4191.66 through bundled Playwright 1.62.1. A click changed displayed state, and WebGL 2 rendered a rectangle with the expected pixel and no graphics error. The reported renderer was ANGLE / Intel Arc Pro Graphics / Direct3D 11, rather than a reported software renderer. This is not a game-performance benchmark. |
| Browser audio processing | An `AudioContext` was running at 48 kHz after a click, and offline rendering produced nonzero sine-wave samples. No sound was sent to physical output. Audible playback, loopback capture, recovery from a suspended context and musical quality remain untested. |
| Administrator access | The current process is not elevated. User-space packages work; an installer that actually requires Windows elevation may need the user. |

Probe files, downloads and explicitly configured temporary/cache locations were
confined to `scratch/capability-audit/` and `scratch/godot-qualification/`.
They are disposable diagnostics, not project dependencies or active work records.

## Hardware and installed software

The machine reports Windows 11 Pro x64, an Intel Core Ultra 9 185H processor
(16 cores, 22 logical processors), approximately 31.4 GiB usable RAM, and
approximately 744 GiB free on the system drive at the time of inspection.

`dxdiag` identifies Intel Arc Pro Graphics with 128 MB dedicated graphics
memory and approximately 18 GB shared memory, with DirectX feature levels
through 12_2. Shared memory should not be treated as equivalent to a discrete
GPU with that much dedicated VRAM. This supports investigating modest scenes;
it does not establish performance in any particular engine.

Unity, Unreal and Blender were not found through PATH, the Windows
uninstall inventory or their standard installation locations. This was not an
exhaustive search for portable copies. Godot Standard was supplied by the producer
and qualified below. Visual Studio Community 2022 is present,
but the targeted `vswhere` query did not find the x86/x64 C++ toolchain component.

The [dependency options review](dependency-options.md) compares official engine
requirements, installation routes and music APIs. Its conclusions make a
browser toolchain and Godot useful first candidates to qualify on this machine.
Unity remains a candidate. Unreal warrants particular performance assessment
because the documented graphics-memory recommendation is not met here.

## Godot qualification

On 12 September 2026, Godot **4.7.2 Standard, Windows x86_64**
(`4.7.2.stable.official.ed1daf0bf`) ran a disposable GDScript scene with three
primitive figures animated by `AnimationPlayer`, a stage, a backdrop, curtains,
a camera and one shadow-casting directional light. This establishes a usable
local engine route for a modest first encounter; it is not a finished gameplay
experiment or an adopted engine decision. The [Godot fit assessment](godot-fit-assessment.md)
provides the wider capability review.

### Rendering and agent iteration

Each renderer ran the same 1280 × 720 scene for 23 seconds, excluding the first
three seconds from measurements. Vsync was disabled for this comparison.
These are application frame intervals and throughput, not monitor refresh
rates, isolated GPU timings or a forecast for a finished game. Both runs were
focused throughout the measured interval.

| Renderer and native driver | Mean frames/s | Median frame, ms | 95th percentile, ms | 99th percentile, ms | Longest frame, ms |
| --- | ---: | ---: | ---: | ---: | ---: |
| Compatibility / OpenGL 3.3 | 1,057 | 0.826 | 1.778 | 2.520 | 4.530 |
| Mobile / Vulkan 1.4.335 | 861 | 1.074 | 1.660 | 2.324 | 28.900 |

Both used the Intel Arc Pro Graphics adapter. No measured frame exceeded
33.33 ms. Compatibility had higher mean throughput; Mobile had slightly lower
95th/99th percentiles. A single run per renderer on this small scene supports
starting with Compatibility, not a general ranking of the renderers. Actual
assets, lighting, navigation and larger scenes need measurement when introduced.

Computer Use captured the rendered scene and clicked a movement button. The
character visibly moved and the event was logged. After editing the source to
change the revision label and player colour, a fresh run showed both changes;
keyboard movement and the audio sequence worked again. The native editor also
imported the project and launched/stopped the scene through its controls.
No Godot error or warning lines appeared in the qualification logs. No engine
MCP, .NET edition or C++ toolchain was needed for these checks.

### Audio, delayed delivery and cancellation

Two interactive runs used synthetic two-second Ogg clips at 120 BPM through
`AudioStreamInteractive`. Reply requests switched on the next beat;
interruptions and departures used immediate transitions with short crossfades.
The application observed reply clip changes 42–506 ms after requests, depending
on beat position, and interruption/departure changes within 38–48 ms. These
observations include application polling and are not physical input-to-sound
latency measurements. Godot reported WASAPI at 48 kHz and approximately 10 ms
output latency; that API value is not an end-to-end guarantee.

A loopback-only HTTP fixture delayed each complete audio response by three
seconds. Godot received four successful responses in 3.07–3.10 seconds across
the two runs. In each run, the current response was decoded and played while
movement remained available. The other response arrived after departure and
return; its obsolete request identifier caused it to be discarded. The
distinctive high notes of the accepted phrase were present in the recorded
output, and absent when the discarded response arrived. This checks complete
phrase buffering and cancellation, not incremental streaming or provider latency.

`AudioEffectRecord` captured the Master bus during each live sequence, producing
approximately 24 seconds of 48 kHz stereo PCM. Both recordings had zero
full-scale samples, peak amplitude below 0.129, and no 10 ms window with RMS
below 0.0001. These bounded measurements found no clipping or sustained silence.
The producer separately confirmed hearing the live test and described the notes
as **"crisp, steady and unbroken"**. This completes the physical audibility and
listening check for the synthetic sequence; it does not establish interactive
input-to-sound latency or the quality of generated vocals.

Fixtures, source, screenshots, JSON measurements and WAV recordings are in
`scratch/godot-qualification/`; run names are `compatibility-a`, `mobile-a`,
`interaction-a` and `interaction-b`. An isolated Python environment with
SoundFile generated and analysed the synthetic fixtures; it is not a game
runtime dependency. Godot's configured logs, application-data and temporary
paths stayed inside that scratch directory. The test editor, game processes
and loopback server were stopped after the checks.

The bounded engine qualification is complete. The separate
[music-provider assessment](music-provider-assessment.md) owns subsequent singing
auditions and encounter evidence. Imported character assets, standalone export
and performance under a representative gameplay workload remain unqualified.

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
- **A concrete paid API decision and secret provision.** The approved ElevenLabs
  trial now has verified Starter access and an encrypted local key; its
  [assessment](music-provider-assessment.md) owns access boundaries and usage.
  New services or further spending still need case-by-case assessment. A
  ChatGPT/Codex plan does not fund third-party game API calls.
- **Actual elevation or app-access prompts.** Respond when a selected installer
  or app presents one. Ordinary package installation has already worked without
  elevation; no broad permissions change is indicated.
- **Musical judgement.** Automated timings, state checks, screenshots and audio
  measurements can support review. They do not establish that a song is funny,
  touching or worth hearing again; that remains part of the producer role.

## Remaining dependency qualification

Godot passed the bounded native rendering, input, edit/rerun, recorded-audio
and producer listening checks above. No additional engine integration is
currently a demonstrated prerequisite for this scope.

The [music-provider trial](music-provider-assessment.md#measured-results) measured
three generated responses and their delivery delays. The producer found all three
clear and acceptable, preferring Take 3. A
[native encounter fixture](music-provider-assessment.md#godot-encounter-assessment)
now exercises three- and ten-second delivery waits, musical entry, movement and
cancellation. Its technical checks passed. The producer found the longer wait
stalled, the shorter wait closer to responsive enough, entry into the recording
OK, and cut-in/departure too abrupt. This supports basic Godot-and-audio
integration; responsive, coherent musical interaction remains unqualified. The
[next capability assessment](music-provider-assessment.md#adaptive-music-capability-assessment)
will review adaptive generation across the evolving scene and propose phased
tests of the required combination of tools and services.
Provider candidates and their access requirements are in the
[dependency options review](dependency-options.md).
