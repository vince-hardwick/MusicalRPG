# Godot fit for Musical RPG

Reviewed on 11 September 2026 against official Godot stable documentation.
This is a provisional dependency assessment, not an adopted engine decision.
The [local qualification](local-development-readiness.md#godot-qualification)
records the subsequent native graphics, input, iteration and audio checks.
The separate [music-provider assessment](music-provider-assessment.md) records
subsequent generated-singing trials and a disposable encounter fixture.
The [agreed brief](https://github.com/vince-hardwick/MusicalRPG/issues/1)
and [role-play decision](../adr/0001-musical-participation-within-role-play.md)
provide the project requirements; source conversations remain orientation only.

## Assessment

Godot is a strong candidate for the first musical encounter. It supplies the
world, movement, animation and audio-playback machinery; we would build the
characters' behaviour and musical direction around it. Its documented tools
support substantial agent authoring and iteration. Local qualification has
established rendering, native input, edit/rerun and recorded-audio behaviour in
a small synthetic scene. The producer confirmed clear, steady and uninterrupted
live audio. Generated singing has since been auditioned in the linked assessment;
representative gameplay and coherent adaptive musical interaction remain unqualified.
Installation convenience is not a selection criterion: the producer is willing
to install the selected software through a normal distribution channel.

Godot is a complete 2D/3D game engine with a scene editor, physics, animation,
scripting, audio and export tools. It is free and open source under the MIT
licence; distributed games need the applicable engine notices. Asset and music
licences remain separate. [Features](https://docs.godotengine.org/en/stable/about/list_of_features.html),
[Godot licence](https://godotengine.org/license/).

## Fit for the integrated graphics

The [local assessment](local-development-readiness.md#hardware-and-installed-software)
records Intel Arc integrated graphics and approximately 32 GB RAM. Godot's
minimum requirements explicitly include integrated graphics for simple 3D
projects and 4 GB RAM for its native editor. Its recommended graphics examples
are still dedicated cards, so the minimum establishes a plausible route, not
a performance promise. [System requirements](https://docs.godotengine.org/en/stable/about/system_requirements.html).

Use Compatibility as the initial renderer to assess: it retains core 3D
features with a low base rendering cost. Advanced features such as volumetric
fog, SDFGI and compute shaders are unavailable. Compare Mobile on the same
scene; despite its name it also targets desktop and can render simple scenes
faster than Forward+. The renderer documentation warns that Compatibility has
higher scaling costs and switching renderers may require scene adjustments.
Choose using measured results rather than assuming one mode is always fastest.
[Renderer comparison](https://docs.godotengine.org/en/stable/tutorials/rendering/renderers.html).

The earlier WebGL probe used ANGLE/Direct3D 11. It did not qualify Godot's
native OpenGL or Vulkan/Direct3D 12 paths. A stylised encounter with a few
performers is a sensible assessment target; dense crowds, elaborate shadows
and a large world would need their own performance work.

## What it can contribute

| Project need | Documented capability and work still required |
| --- | --- |
| Characters moving around an encounter | `NavigationAgent3D` supplies pathfinding and avoidance helpers. Our scripts still move the actor and decide its destination, purpose and response to the player. A navigation agent is not an intelligent RPG character. [Navigation agents](https://docs.godotengine.org/en/stable/tutorials/navigation/navigation_using_navigationagents.html). |
| Walking, gesturing and theatrical staging | `AnimationPlayer` supplies animation tracks; `AnimationTree` supplies blending, layered animations, one-shot gestures and state transitions. These are useful foundations for movement and performances, but animation clips, staging and interruption logic remain game-development work. [AnimationTree](https://docs.godotengine.org/en/stable/tutorials/animation/animation_tree.html). |
| Responding while the player remains free | Signals let objects notify other objects of events. We must implement what an interruption, departure or chosen player intention means, including cancelling obsolete musical responses and preserving consequences. The engine does not impose a locked cutscene. [Signals](https://docs.godotengine.org/en/stable/getting_started/step_by_step/signals.html). |

Godot recommends glTF/GLB for imported 3D scenes and supports FBX. Direct
`.blend` import requires Blender because Godot invokes its exporter; using
already-exported GLB assets avoids that requirement. Skeleton retargeting can
share animations across characters, but bone names alone do not guarantee
compatible poses. Asset selection, licences and rig quality need assessment
when concrete assets are chosen. [3D formats](https://docs.godotengine.org/en/stable/tutorials/assets_pipeline/importing_3d_scenes/available_formats.html),
[retargeting](https://docs.godotengine.org/en/stable/tutorials/assets_pipeline/retargeting_3d_skeletons.html).

## Musical responsiveness

`AudioStreamInteractive` switches between clips immediately, on the next beat
or bar, or at a clip's end, with fades and optional filler clips.
`AudioStreamSynchronized` starts multiple streams together. These directly suit
the accepted idea of an immediate character reaction followed by a sung reply
at a natural musical break. They require suitable clips and timing metadata;
they do not create compatible music or neural singing.
[Interactive audio](https://docs.godotengine.org/en/stable/classes/class_audiostreaminteractive.html),
[synchronised audio](https://docs.godotengine.org/en/stable/classes/class_audiostreamsynchronized.html).

Downloaded audio can enter the game at runtime: `HTTPRequest` returns response
bytes on completion, and `AudioStreamMP3.load_from_buffer()` creates a playable
resource from MP3 bytes. This establishes a route for complete generated phrases,
not proof that arbitrary partial MP3 chunks can play seamlessly as they arrive.
[HTTPRequest](https://docs.godotengine.org/en/stable/classes/class_httprequest.html),
[MP3 loading](https://docs.godotengine.org/en/stable/classes/class_audiostreammp3.html).

Incremental delivery needs additional integration. `HTTPClient` can read response
chunks; `AudioStreamGeneratorPlayback` accepts raw audio frames and reports buffer
underruns. Transport framing, decoding, sample-rate matching, buffering and
cancellation remain our work. Godot recommends C# or compiled extensions for
demanding sample generation; smaller buffers reduce delay but increase the risk
of crackling. GDScript is therefore a reasonable starting candidate for gameplay
and clip playback, with the audio path measured before choosing extra dependencies.
[HTTPClient](https://docs.godotengine.org/en/stable/classes/class_httpclient.html),
[generator playback](https://docs.godotengine.org/en/stable/classes/class_audiostreamgeneratorplayback.html),
[generator constraints](https://docs.godotengine.org/en/stable/classes/class_audiostreamgenerator.html).

Background work must respect Godot's threading boundaries: the active scene tree
is not thread-safe. Audio timing APIs expose mix timing and output latency, but
cannot eliminate provider or network delay. The separate
[music-provider assessment](dependency-options.md#generated-sung-contributions)
remains relevant regardless of engine choice.
[Thread safety](https://docs.godotengine.org/en/stable/tutorials/performance/thread_safe_apis.html),
[AudioServer](https://docs.godotengine.org/en/stable/classes/class_audioserver.html).

The archived MIDI proposals also need separate assessment: Godot documents
MIDI input but no built-in MIDI output. A MIDI-driven synthesis route would
require additional integration. [Audio features](https://docs.godotengine.org/en/stable/about/list_of_features.html#audio).

## Agent authoring and observation

Scenes can use readable `.tscn` files; scripts can also execute inside the editor.
The CLI supports project/scene runs, imports, exports, script checks, logs and
debugging. These provide a credible authoring loop without making an engine MCP
a prerequisite. A bridge should be assessed if it fills a demonstrated input or
observation gap. The local qualification exercised CLI authoring, native
observation/input and an editor launch; exports and editor scripting remain
documented options rather than exercised capabilities.
[Scene format](https://docs.godotengine.org/en/stable/engine_details/file_formats/tscn.html),
[editor scripts](https://docs.godotengine.org/en/stable/tutorials/plugins/running_code_in_the_editor.html),
[CLI](https://docs.godotengine.org/en/stable/tutorials/editor/command_line_tutorial.html).

`AudioEffectRecord` on the Master bus can record all Godot output to WAV;
`AudioEffectCapture` exposes raw samples for analysis. Neither establishes what
reaches the physical speakers. Headless mode uses dummy audio, and movie capture
renders offline without audible playback during recording. A clean log or smooth
movie therefore cannot prove live timing, performance or musical appeal.
[Audio recording](https://docs.godotengine.org/en/stable/classes/class_audioeffectrecord.html),
[sample capture](https://docs.godotengine.org/en/stable/classes/class_audioeffectcapture.html),
[CLI](https://docs.godotengine.org/en/stable/tutorials/editor/command_line_tutorial.html),
[movie capture](https://docs.godotengine.org/en/stable/tutorials/animation/creating_movies.html).

## Distribution and initial setup

The official Windows download currently lists Godot 4.7.2, dated 18 August
2026, in standard and .NET editions. Recommend assessing the standard x86_64
edition with GDScript, Godot's built-in scripting language, for the initial
gameplay and clip-playback work. The .NET edition adds C# support if later
requirements justify it. [Windows downloads](https://godotengine.org/download/windows/).

The usual direct download is self-contained by design. Godot also links official
Steam, Epic Games Store and itch.io distributions; Steam is a normal managed
installation option if selected. Store versions exclude .NET/C# support. The
producer can choose the installation channel; portability is not part of the
engine-fit recommendation. Export templates are a separate download when needed.
[Distribution options](https://godotengine.org/download/windows/),
[official Steam listing](https://store.steampowered.com/app/404790/Godot_Engine/).

## Target and smallest useful qualification

Recommend assessing native Windows first. Godot web export requires Compatibility
rendering/WebGL 2; current Godot 4 C# projects cannot export to web. Browser Sample
audio lacks effects and procedural generation; Stream mode restores features with
latency and threading trade-offs. A web build is possible to assess separately,
but is not automatically equivalent to the native musical experience.
[Web export](https://docs.godotengine.org/en/stable/tutorials/export/exporting_for_web.html).

The local qualification used the following scope before substantive gameplay
work; the linked readiness document owns its results and remaining checks:

1. Run a rendered scene with a few animated actors and record frame timing under
   the intended camera and lighting; compare suitable renderers on this laptop.
2. Apply player input, observe a visible reaction and logged state change, edit
   the source and repeat to establish the agent's complete iteration loop.
3. Play and record short musical clips, transition between them, and interrupt
   or leave while playback continues. Include a producer listening check.
4. Load a new phrase at runtime with deliberately delayed delivery. Establish
   buffering and cancellation behaviour before a separately assessed paid trial
   measures actual generated singing.

These checks test engine fit. The agreed first playable must still demonstrate
event-specific singing, meaningful consequences and the desire to play again.
