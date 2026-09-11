# Development dependency options

Reviewed against official documentation on 11 September 2026. This is research
for dependency assessment, not an engine selection, implementation plan or
authorisation to install software or spend money. No engine installation or
music API call was made for this review. Recheck the selected versions and
account terms when provisioning; the linked documentation can change.

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

These are candidates for measurement, not adopted providers. None of the
documentation reviewed establishes the end-to-end delay, lyric intelligibility
or character consistency that this particular game will achieve.

| Candidate | What the official interface establishes | Access and unresolved work |
| --- | --- | --- |
| ElevenLabs Music | `music_v2` composition plans accept lyrics, styles and section durations. Documented chunks can be as short as three seconds. The detailed streaming endpoint returns audio chunks and optional word timestamps. Streaming transport alone does not establish how soon the first usable sung phrase arrives. | The Music API quickstart says paid users only and requires an API key. Review the applicable plan, billing and output-use terms before a bounded trial. Measure first playable audio, exact lyric delivery, transitions and voice consistency. [composition plans](https://elevenlabs.io/docs/eleven-api/guides/how-to/music/composition-plans), [detailed stream](https://elevenlabs.io/docs/api-reference/music/compose-detailed-stream), [quickstart](https://elevenlabs.io/docs/eleven-api/guides/cookbooks/music), [pricing](https://elevenlabs.io/pricing/api). |
| Google Lyria 3.5 / Lyria 3 Clip | The Gemini API accepts custom lyrics. Clip produces 30 seconds; Lyria 3.5 generates full songs. The guide describes single-turn generation and says iterative editing through successive prompts is unsupported. This is not evidence of a continuously steerable sung dialogue service. | Both are paid API candidates: the reviewed price page lists $0.08 per Lyria 3.5 song and $0.04 per Clip request, with no free API tier for these models. A Gemini API project/key and Cloud Billing access are needed. Account eligibility and actual generation behaviour remain untested. [generation guide](https://ai.google.dev/gemini-api/docs/music-generation), [pricing](https://ai.google.dev/gemini-api/docs/pricing), [billing](https://ai.google.dev/gemini-api/docs/billing). |
| Google Lyria RealTime | Experimental streaming music can be continuously steered, but the current documentation explicitly limits it to instrumental music. | A possible accompaniment candidate; it does not satisfy the sung-contribution requirement by itself. API access and performance would need testing if shortlisted. [RealTime guide](https://ai.google.dev/gemini-api/docs/realtime-music-generation). |

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

Before gameplay implementation, the smallest useful dependency qualification is
one selected toolchain that can run a rendered scene, accept input, expose a
state change, play and capture sound, and repeat after a source edit. Separately,
an authorised short music trial should establish whether an event-specific
sung contribution is usable. These checks remain proposed assessment work;
this note makes no engine or service commitment.
