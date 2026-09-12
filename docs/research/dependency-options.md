# Development dependency options

Engine options reviewed against official documentation on 11 September 2026;
music-provider research and qualification pointers updated on 12 September 2026.
This is dependency research, not a permanent engine selection or authorisation
to install software or spend money. Local execution evidence belongs in the
[readiness assessment](local-development-readiness.md). Recheck selected versions
and account terms when provisioning; the linked documentation can change.

## What the development loop needs

The dependency question extends beyond whether an editor will install. Astra
needs to create and change content, launch the result, supply player input,
observe the resulting game state and rendered scene, capture the audio, and
repeat the encounter. A successful build or headless test does not establish
that the music is audible, intelligible or entertaining.

There is no general requirement for a human to install every third-party
dependency. Some packages have command-line installation routes, and Godot has
a portable executable. Account authentication, payment setup, licence choices
and any Windows elevation prompt are separate constraints. Documentation of
an installation route is not evidence that it has worked on this machine.

## Game development options

The [Godot fit assessment](godot-fit-assessment.md) examines its graphics,
animation, musical timing and autonomous iteration against this project's brief.
Godot has now passed the bounded [local qualification](local-development-readiness.md#godot-qualification);
the table below describes the broader dependency options, not their local results.

| Candidate | Windows dependencies and hardware | Installation and observation route |
| --- | --- | --- |
| Browser game using TypeScript, a renderer such as Three.js, and Web Audio | A supported Node.js runtime, project packages and a modern browser. Vite documents Node 20.19+ or 22.12+; current Playwright documents recent 22.x, 24.x or 26.x and Windows 11+. Three.js's WebGL renderer requires WebGL 2. These are tool requirements, not a guarantee of scene performance. | Vite provides npm installation, a local development server and production builds. Playwright supports browser input and inspection, screenshots, traces, and headed or headless runs. It can use installed Edge or Chrome. This gives a documented route for an automated browser play loop without a desktop game editor. [Vite](https://vite.dev/guide/), [Three.js](https://threejs.org/docs/pages/WebGLRenderer.html), [Playwright installation](https://playwright.dev/docs/intro), [browser support](https://playwright.dev/docs/browsers). |
| Godot | Standard Windows download is self-contained: extract and run. Its documented simple-project minimum is Windows 10, 4 GB RAM and integrated graphics supporting the chosen renderer: OpenGL 3.3 for Compatibility, or Vulkan 1.0 for Forward+/Mobile. The recommendation is 8 GB RAM and stronger graphics. Export templates are a separate download, about 1.3 GB installed. | CLI supports running projects and scripts, importing/exporting, logs and movie capture. `--headless` uses a dummy audio driver, so it cannot verify audible playback. The portable download avoids a conventional installer; actual execution and graphics compatibility still need a local check. [Windows download](https://godotengine.org/download/windows/), [system requirements](https://docs.godotengine.org/en/stable/about/system_requirements.html), [CLI](https://docs.godotengine.org/en/stable/tutorials/editor/command_line_tutorial.html). |
| Unity | Unity 6.3 LTS documents Windows 10 21H1+ on x64, SSE2, supported graphics drivers and DX10/11/12 or Vulkan graphics; at least 8 GB RAM is recommended. Windows IL2CPP builds add C++ tools and a Windows SDK. Modules depend on the target platform. | Hub has an experimental headless CLI for Editor and module installation. Hub sign-in activates an eligible Personal licence; obtaining one may require accepting its terms. Editor batch mode and the Test Framework support scripted builds and tests. `-nographics` disables the graphics device: use a rendered run for visual evidence. Native player control/capture or a suitable integration still needs proving. [requirements](https://docs.unity3d.com/6000.3/Documentation/Manual/system-requirements.html), [Hub CLI](https://docs.unity.com/en-us/hub/use-hub-cli), [licences](https://docs.unity.com/en-us/hub/manage-license), [Editor CLI](https://docs.unity3d.com/6000.3/Documentation/Manual/EditorCommandLineArguments.html), [test CLI](https://docs.unity3d.com/6000.3/Documentation/Manual/test-framework/reference-command-line.html). |
| Unreal Engine | The current UE5 requirements page recommends Windows 11, a quad-core 2.5 GHz processor, 32 GB RAM, 8 GB graphics RAM and DX12 graphics. Advanced rendering features have additional requirements. C++ development adds the compatible Visual Studio toolchain; prerequisites accompany the Launcher install. | Launcher download requires Epic sign-in. The offline silent installer is restricted to approved organisations or those with purchased seats, so it is not a universally available unattended shortcut. Editor Python commandlets and command-line automation tests provide useful automation; Python editor scripting is not a runtime gameplay API. Native play, capture and performance need separate qualification. [requirements](https://dev.epicgames.com/documentation/unreal-engine/hardware-and-software-specifications-for-unreal-engine), [installation](https://dev.epicgames.com/documentation/en-us/unreal-engine/install-unreal-engine), [offline installer](https://dev.epicgames.com/documentation/en-us/unreal-engine/offline-installer-of-unreal-engine), [Python scripting](https://dev.epicgames.com/documentation/en-us/unreal-engine/scripting-the-unreal-editor-using-python), [automation tests](https://dev.epicgames.com/documentation/en-us/unreal-engine/run-automation-tests-in-unreal-engine). |

Browser audio also needs a real playback check. Chrome can suspend an
`AudioContext` until the user interacts with the page. Web Audio supplies
scheduling and processing facilities; it does not itself generate intelligible
sung lyrics. [Chrome autoplay policy](https://developer.chrome.com/blog/autoplay),
[Web Audio specification](https://webaudio.github.io/web-audio-api/).

## Generated sung contributions

The [music-provider assessment](music-provider-assessment.md) owns the current
shortlist, API contracts, entry costs, output-use constraints and approved
three-render trial. It favours ElevenLabs Music for the first short reply,
retains Google Lyria Clip as a possible comparison, and distinguishes Lyria
RealTime's instrumental generation from sung contributions. Three ElevenLabs
requests succeeded; the linked note owns measured delivery delays and usage.
The producer found all three clear and acceptable, preferring Take 3. A Godot
fixture now exercises waiting, musical entry and cancellation with that saved
take. The producer found entry acceptable, the longer wait stalled, and cut-in
and departure too abrupt; the shorter wait was closer to responsive enough.
This establishes a basic integration exercise, with musical exits and
responsiveness still unresolved. No permanent provider choice or repeatable
character identity has been established.

Development-agent usage and a game's runtime API usage are distinct. OpenAI's
documentation separates ChatGPT usage controls from API Platform billing and
states that API-key Codex access uses API token pricing. A ChatGPT/Codex plan or
usage reset should therefore not be counted as funding for game API calls.
[OpenAI usage controls](https://learn.chatgpt.com/docs/enterprise/usage-limits),
[Codex billing distinction](https://learn.chatgpt.com/docs/agent-configuration/speed).

## Tool access and human involvement

An MCP, plugin or skill is useful when it fills a demonstrated gap in the loop.
The documented CLI routes above already provide substantial authoring and test
automation. An engine bridge must additionally prove that it can control the
running encounter and return useful state and visual evidence; an installation
alone is insufficient. No third-party engine bridge was selected or tested in
this review. ElevenLabs publishes a music skill linked from its quickstart;
that is a candidate convenience, not a substitute for API access or cost review.

The likely human steps are conditional on the eventual shortlist:

- Sign in, complete MFA and resolve account eligibility when a service or
  engine requires them. Unity and Epic account flows are relevant only if
  those engines are selected.
- Select and enable any paid music/API access after reviewing a concrete
  provider and estimated trial cost. Make credentials available through the
  chosen secret mechanism, not repository source or a public browser bundle.
- Respond to an actual Windows elevation or security prompt if an installation
  requires it. Do not assume every package needs administrator privileges.
- Listen to playable output and judge musical appeal. File existence, waveform
  analysis, timings and even transcription are useful evidence but do not
  establish that a performance is enjoyable.

The bounded Godot qualification is complete; its scope and limits are recorded
in the readiness assessment linked above. The music-provider assessment records
the completed three-render trial, positive producer audition and contextual
feedback on the Godot fixture. Its [next assessment](music-provider-assessment.md#adaptive-music-capability-assessment)
examines API capabilities and a phased route to coherent music generated in response
to an evolving scene. The accepted cut-in/departure revision remains a small
integration check within that broader question.
