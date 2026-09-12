# Adaptive music capability assessment

Reviewed against public primary sources on 12 September 2026. This is research
and a proposed assessment programme, not an adopted architecture, provider choice
or authority for further paid calls. The [existing provider assessment](music-provider-assessment.md)
owns the completed trial, producer verdict and account boundaries. The
[interaction decision](../adr/0001-musical-participation-within-role-play.md)
keeps musical participation inside ongoing role-play.

## Recommendation and scope

**Test contextual ElevenLabs continuations first on the existing Godot setup,
while qualifying a score-controlled singing route as the stronger control
alternative.** Keep Godot's existing scheduling and audio facilities as the
comparison baseline. Add another music service or middleware only when a test
identifies a specific gap that it can address. No reviewed public offering yet
establishes the complete combination of event-specific lyrics, independent
character singing and all five kinds of coherence through repeated live changes.
This is a finding about available evidence, not a claim of impossibility.

The most useful alternatives serve different roles:

- **Locally controlled notes and accompaniment**, paired with an accessible
  score-driven singing engine, offer the clearest mechanism for synchronising
  harmony, motifs and participants. The singing runtime's availability, terms
  and response time are unresolved.
- **Lyria RealTime** offers cloud instrumental steering, with explicit limits
  around tempo and scale changes. It needs a separate singing solution.
- **Magenta RealTime 2** adds genuine MIDI conditioning to real-time instrumental
  generation. It is a significant comparator, conditional on supported hardware;
  the existing Windows laptop has not been qualified for it.

The [phased plan](#phased-assessment-plan) compares those routes without treating
the proposed division of responsibilities as adopted architecture. Its earliest
paid experiment is two successive contextual continuations, preceded by a source,
access and cost check. No further generation, upload, stem extraction, finetune,
subscription, purchase or vendor contact was performed in this research.

## Recovered intent and source limits

All four complete [tracked source captures](../reference/source-chats/README.md)
were read, including both user prompts in the initial ChatGPT share. The original
Codex task **Review MusicalRPG AI tooling**, ID
`01a09002-6e49-7560-93a4-2b2b59654112`, was read with pagination to recover the
initial request and the Q1–Q7 grilling exchanges and acceptances. The closing
confirmation is in turn `01a0903f-17a3-7c72-bd07-a6ca8268e7e7`.
Live [issue #1](https://github.com/vince-hardwick/MusicalRPG/issues/1) was verified
open, with no comments or labels, and remains the accepted first-playable brief.

| Source | What informs this assessment |
| --- | --- |
| [Initial ChatGPT share capture](../reference/source-chats/chatgpt-initial.md) | The system should construct performances from world facts, support player contributions that change outcomes, and survive missing or disrupted performers. Suggested villages, weekend scope and six-system architecture were examples, not adopted limits or architecture. |
| [Continuation capture](../reference/source-chats/chatgpt-continuation.md) | Corrects the dictated model name to Astra; emphasises creative freedom and build–run–observe–revise with the human as producer. A fixed demonstration would miss the experiment. Only one response is exposed; its preceding prompt is unavailable. |
| [MusicalRPG 1](../reference/source-chats/musicalrpg-1.md) | Proposes separate scene/lyric, composition, singing and playback roles; includes a second NPC joining a solo. Its claimed API availability and zero latency require verification. |
| [MusicalRPG 2](../reference/source-chats/musicalrpg-2.md) | Proposes cloud lyric generation and local synthesis/middleware. Its missing mockup, old model ID and asserted timings are not evidence of a working pipeline. |
| Initial grilling and [routed brief](https://github.com/vince-hardwick/MusicalRPG/issues/1) | Unexpected actions become musical material; intentions produce sung contributions and consequences; movement, interruption and departure remain possible. Simple accompaniment and imperfect staging are acceptable. Assess entertainment and required producer intervention separately. |

The Google Docs are captured Gemini responses without their original user
prompts. Those missing turns have not been reconstructed, and the four documents
were reviewed through their complete 11 September captures rather than recaptured
from the services. Their index owns the live URLs and capture limitations.

The producer's [current adaptive brief](music-provider-assessment.md#adaptive-music-capability-assessment)
requires adaptation to player actions, NPC actions and dynamic scene elements,
including expected and responsive transitions. Preparation during an anticipated
approach can help expected events; an unanticipated action must still cause new,
relevant musical material. The accepted quality compromises do not remove that
requirement. Improving the saved take's exit remains a limited integration check.

## What has to remain coherent

These are proposed assessment criteria derived from that brief. A common key,
nominal BPM or smooth crossfade is insufficient by itself.

| Dimension | Required observable behaviour | Smallest useful challenge |
| --- | --- | --- |
| Harmonic | Parts agree with the harmony at their actual entry; tension and resolution make sense. | Introduce a response over a changing chord progression, then request a deliberate modulation. Check voice leading and chord position as well as key. |
| Melodic | An original motif remains recognisable and can develop or return with new words. | Repeat or transform a short motif after another singer joins and after the generator's short audio context has elapsed. |
| Rhythmic | Pulse, metre, bar position and lyric stresses fit together without cumulative drift. | Add a part between beats; later change tempo or metre. Judge pickups, syncopation and intentional rubato as musical choices, not automatic errors. |
| Compositional | Phrases, breaths, cadences and sections form an intelligible performance through changes. | Interrupt before a planned cadence and require a convincing continuation or transition rather than an unrelated restart. |
| Thematic | Music and words express the current dramatic aim, character and consequences, with meaningful reprises. | Reverse the player intention, let an NPC act independently, and later recall the changed outcome without repeating obsolete claims. |

Also assess intelligibility, repeatable singer identity, independent participation,
useful response time and continued player agency. A newly audible second voice
does not establish a separately controllable character part. Lyrics that mention
an event do not alone establish harmonic or melodic adaptation.

## Evidence labels

**Documented** means an exposed contract or workflow; **provider claim** means
an advertised musical result; **measured** refers to the retained local trial;
**inference** identifies reasoning from those sources; **untested** marks the
remaining experimental question. Public documentation is dated evidence and can
change. Account access and usable quotas are distinct from a public endpoint.

## ElevenLabs: contextual generation is plausible; continuous control is unqualified

**Recommendation:** retain Music v2.5 for the first test of *successive contextual
adaptations*. Its documented continuation and inpainting facilities are materially
more relevant than another isolated sung phrase. Do not yet make it the sole
runtime composer: the reviewed API does not establish that an ongoing render can
accept new musical instructions, that separate generations share an exact score,
or that successive singers retain identity. A working combination will need an
explicit musical timeline and a policy for material already committed to playback.
This is an engineering inference from the interfaces below, not proof that the
provider cannot support a richer arrangement through another offering.

### What the Music API actually offers

| Surface | Documented capability | Consequence for this project |
| --- | --- | --- |
| Composition plans | `music_v2_5` and `music_v2` take ordered chunks with lyric `text`, `duration_ms`, positive/negative styles and `context_adherence`. Limits: 30 chunks, 3–120 seconds per generation chunk, 3–600 seconds per song. [Guide](https://elevenlabs.io/docs/eleven-api/guides/how-to/music/composition-plans) | Expected scene development, contrasting sections and multi-part arrangements can be submitted together. A chunk is a planned song section, not a promise of one promptly playable transport packet. |
| Plan generation | `/v1/music/plan` can derive a new plan from a prompt and optional source plan. Documentation says it costs no credits but is rate limited. [Reference](https://elevenlabs.io/docs/api-reference/music/create-composition-plan) | Useful for planning successive scene responses. Revising a plan does not revise audio already rendered. |
| Streaming and details | `/v1/music/stream` returns audio; `/v1/music/detailed/stream` returns SSE with audio, composition information, metadata, optional word timestamps and completion. `seed` is best effort; a Music `finetune_id` is accepted. [Detailed stream](https://elevenlabs.io/docs/api-reference/music/compose-detailed-stream) | Enables a client to consume arriving audio and align captions. Neither timestamps nor streaming specify a musical clock or a first-audible-word deadline. |
| Retained audio and inpainting | Plans can insert unchanged ranges from a stored `song_id`, interleaved with new generation chunks. The official guide demonstrates section replacement, extension and a new transition between two retained slices to form a loop. [Inpainting](https://elevenlabs.io/docs/eleven-api/guides/how-to/music/inpainting) | Strongest candidate for carrying an audible musical scene into a new response. This is a new render using context; the game must schedule its usable continuation. |
| Audio conditioning | A generated chunk can reference up to 30 seconds of stored audio with `conditioning_ref`; `condition_strength` runs from low through `xhigh`. `context_adherence` controls consistency with neighbouring chunks. [Inpainting](https://elevenlabs.io/docs/eleven-api/guides/how-to/music/inpainting) | Test whether it preserves melody, harmonic direction, groove and singer character while changing the lyric. Similarity controls do not state exact note preservation. |
| Upload | `/v1/music/upload` returns a stored song ID. Optional plan extraction and lyric timestamps add latency. Upload is charged like generation; copyright rejection still incurs half the request cost. [Upload](https://elevenlabs.io/docs/api-reference/music/upload) | Saved trial audio might supply context after an approved upload. A usable stored ID has not been established by this review. Uploading is a paid operation, not a free preflight. |
| Stems | `/v1/music/stem-separation` accepts a complete file and returns a ZIP; the reference exposes `two_stems_v1` and `six_stems_v1`, defaulting to six. It warns of potentially high latency. [Reference](https://elevenlabs.io/docs/api-reference/music/separate-stems) | Potentially separates vocals from accompaniment for spatial character audio or independent mixing. It is post-processing, not simultaneous streamed generation of independent singer parts. |
| Video to music | Uploaded videos plus optional text/styles produce a matching background track. [Reference](https://elevenlabs.io/docs/api-reference/music/video-to-music) | Potentially useful for fixed cinematics; no documented live world-event input loop. |

The public Python SDK was inspected at commit
[`bc7f996e5a0a92a5b1feb09503a89db0dd70dc83`](https://github.com/elevenlabs/elevenlabs-python/tree/bc7f996e5a0a92a5b1feb09503a89db0dd70dc83).
Its [Music raw client](https://github.com/elevenlabs/elevenlabs-python/blob/bc7f996e5a0a92a5b1feb09503a89db0dd70dc83/src/elevenlabs/music/raw_client.py#L420)
submits the detailed stream's complete JSON request once by HTTP POST, then reads
the response. The inspected Music client has no append/update/cancel-generation
method or Music WebSocket session. Closing playback or abandoning a response
should not be assumed to stop server computation or billing. An unexpected action
therefore calls for another request under this documented interface. Audio already
heard cannot be revised; audio buffered locally can only be replaced before playback.

### Musical control: favourable claims need direct tests

The provider's [prompting guide](https://elevenlabs.io/docs/overview/capabilities/music/best-practices)
claims BPM and key adherence sufficient to layer generated material, suggests
multiple singers harmonising, supports a cappella or solo-instrument prompts,
and describes arrangement changes after specified bars. These are meaningful
reasons to test a combined route. The same guide says key is *often* captured and
audio references preserve feel, groove and palette without copying notes; its
stronger assertions about exact numerical control should not become project guarantees.

The inspected [generation-chunk schema](https://github.com/elevenlabs/elevenlabs-python/blob/bc7f996e5a0a92a5b1feb09503a89db0dd70dc83/src/elevenlabs/types/generation_chunk_input.py)
contains text, duration, styles and context/reference controls. It exposes no
typed MIDI/score input, note pitches/onsets, chord sequence, key, BPM, time
signature, syllable-to-note mapping, motif identifier or per-singer voice/track
assignment. Key, chords, meter, melodic shape, cadence and a cappella delivery can
be requested in prose; their precision and repeatability remain experimental.
Duration enforcement is stronger: the SDK's [compose contract](https://github.com/elevenlabs/elevenlabs-python/blob/bc7f996e5a0a92a5b1feb09503a89db0dd70dc83/src/elevenlabs/music/raw_client.py#L331)
states that v2-family section durations are enforced. A twelve-second section
still does not specify where its downbeat or first consonant occurs.

Consequently, thematic/style continuity is well aligned with the interface;
compositional continuity has section/context tools; harmonic, rhythmic and melodic
continuity need listening and analysis. Two independently generated tracks can
share key and nominal tempo while disagreeing on chord position, metre phase,
cadence or melodic destination. That synchronization risk is an inference, not a
claim that the advertised layering cannot work. In particular, generated harmony
between two singers in one mix does not establish independently controllable
characters joining and leaving an existing performance.

### Singer identity and the rest of ElevenLabs

Music Finetunes learn a dataset's style, instrumentation, rhythmic feel, timbre
and vocal character; the provider says training typically takes 5–10 minutes.
They are intended to support recurring sonic identity, including game soundtracks.
They do not promise exact melody, character identity across arbitrary register
changes, or individually assigned singers. [Music overview](https://elevenlabs.io/docs/overview/capabilities/music)
and [finetune guide](https://elevenlabs.io/docs/eleven-creative/products/music/finetunes).
The public [create API](https://elevenlabs.io/docs/api-reference/music/finetunes/create)
supports uploaded training files, model selection and private/workspace visibility;
generation accepts one finetune ID at request level. However, the product guide
still describes API access as potentially Enterprise-only on request. Public schema
availability does not prove the current Starter account can use it.

| Related capability | Useful contribution and limit |
| --- | --- |
| Voice Design | Generates previews and saves a selected voice for reuse. [Guide](https://elevenlabs.io/docs/eleven-api/guides/how-to/voices/voice-design) This supports a character voice library for compatible speech/conversion endpoints; Music does not accept the resulting ordinary `voice_id`. |
| TTS and dialogue | Eleven v3 supports expressive speech and an experimental `[sings]` tag; effectiveness varies by voice. [TTS guidance](https://elevenlabs.io/docs/overview/capabilities/text-to-speech/best-practices) It merits a narrow recitative/vocal experiment if needed, but supplies no documented score-following contract. Speech latency figures do not transfer to Music. |
| Voice Changer | Accepts a source performance and target `voice_id`; it aims to preserve timing, emotion and delivery. Streaming requires an uploaded audio input. [Capability](https://elevenlabs.io/docs/overview/capabilities/voice-changer), [API](https://elevenlabs.io/docs/api-reference/speech-to-speech/stream). A separate source must already supply the sung notes and words. |
| Singing Voice Changer marketing | The provider explicitly markets [singing voice conversion](https://elevenlabs.io/voice-changer/singing). Treat this as a candidate for testing identity over an existing sung performance, not proof of note accuracy, sustained-vowel quality, low latency or end-to-end spontaneous singing. |

A Music-to-stems-to-Voice-Changer chain is therefore plausible but untested. It
adds sequential processing and potential separation/conversion artefacts. A
score-driven singer could instead supply the performance to conversion; that
requires a separately qualified synthesiser. Speech recognition, dialogue and
sound effects can support world interaction, but do not themselves supply a
shared harmonic and melodic plan.

### Responsiveness and experiment boundaries

The existing [measured-results owner](music-provider-assessment.md#measured-results)
records that each of the three twelve-second trials arrived as **one whole audio
chunk**. Complete decoded audio became available in 2.78–9.76 seconds. Those
observations do not characterize contextual extension, longer streams, stems or
conversion. The official [Music streaming example](https://elevenlabs.io/docs/eleven-api/guides/how-to/music/streaming)
also buffers everything before its playback helper; copying it would not measure
incremental playback. No numeric Music first-word service guarantee was found in
the reviewed contract.

For a retained-source continuation, measure time to the **first usable new
material**, not merely to re-emitted old audio. Also measure prefix processing,
first decodable packet, first sung word, available musical lead, buffer underruns
and the actual seam. Test whether the new continuation arrives before its planned
entry; an excellent offline edit that routinely misses that entry fails the
runtime purpose. Repeated adaptations must be heard in sequence rather than
judged as separately successful songs.

Current [ElevenAPI pricing](https://elevenlabs.io/pricing/api) lists Music at
$0.15/minute, finetunes at $1.50 each, and Voice Changer at $0.12/minute, before
taxes. These headline rates do not resolve short-request rounding, interrupted
requests, or charging retained versus newly generated duration in inpainting.
The older [feature announcement](https://elevenlabs.io/blog/eleven-music-new-tools-for-exploring-editing-and-producing-music-with-ai)
prices two-stem separation at half generation cost and four stems at generation
cost; it does not settle today's API six-stem price. Do not price a proposed
runtime chain using only its final audible duration.

The [model-specific terms](https://elevenlabs.io/eleven-music-model-specific-terms)
list Starter API access including stems/streaming/timestamps and two concurrent
generations. They exclude monetised games available through multiple platforms
from self-serve media rights, define third-party music-streaming distribution
separately from HTTP streaming, and restrict output libraries. Their allowance
table differs from current API pricing. [Music API terms](https://elevenlabs.io/music-api-terms)
also permit staggered feature access and distinguish a substantive application
from restricted resale/model aggregation. The existing local trial is not release
clearance. Retain account-specific verification and output-use review as
prerequisites for the relevant later experiment or distribution step.

Other inconsistencies to preserve: the overview still states a five-minute maximum
against the plan/API ten-minute limit; API defaults still specify `music_v1`;
the website advertises two/four/six stem options while the API exposes two/six;
and finetune API documentation is ahead of its product-guide access wording.
Pin `music_v2_5` and an explicitly supported stem format in any approved test.

The earliest discriminating paid candidate is a **retained-source branch chain**:
continue an existing performance in response to an unplanned intention, then
adapt that new continuation again to an NPC action. Compare continuity and actual
entry feasibility before adding a second singer or a processing chain. Confirm a
usable stored source ID or price one upload first. The prior requests explicitly
set `store_for_inpainting=false`; a returned song ID alone does not establish
reference reuse. Prepare the exact requests and charging assumptions for
producer approval. The completed three-request authority covers none of these
operations. This test can falsify the leading ElevenLabs route without pretending
that a good independent phrase or a smoother fade establishes adaptive composition.

## Alternatives recovered from the sources

### Continuous generative accompaniment

**Lyria RealTime** (`models/lyria-realtime-exp`) supports a persistent
bidirectional music stream, weighted prompts and updated generation settings.
Its configuration includes BPM, scale, density, brightness, guidance and
bass/drum controls. It does not expose a chord timeline, melody-note sequence,
lyrics, bar position or independently addressable musical parts. The guide's
MIDI controller example is not direct MIDI-note conditioning. [Guide](https://ai.google.dev/gemini-api/docs/realtime-music-generation),
[SDK configuration](https://googleapis.github.io/js-genai/release_docs/interfaces/types.LiveMusicGenerationConfig.html).

Gradual prompt changes can steer an ongoing stream, but drastic changes may be
abrupt. BPM or scale changes require `reset_context()`, which the guide calls a
hard transition. Scale choices combine relative major/minor; they do not select
tonic and mode independently. The model is explicitly instrumental:
`VOCALIZATION` means voice-like sounds, not supplied sung words. There is no
documented numeric action-to-audible-change guarantee. **Disposition:** test for
continuous accompaniment while holding tempo and pitch collection fixed, then
test the reset boundary separately. It cannot be assumed to follow a separate
singer's chord progression. [RealTime controls and limitations](https://ai.google.dev/gemini-api/docs/realtime-music-generation).

**Magenta RealTime 2**, released in June 2026, materially advances the earlier
Magenta suggestion. It adds MIDI conditioning and 40 ms audio frames; its
approximately 200 ms control latency is a provider-reported figure, not a local
measurement. The model card describes a 20-second effective audio receptive
field and per-frame control of 128 MIDI pitches as off, sustain, onset or model
choice. It is instrumental, with occasional non-lexical vocal sounds. This is
an actual pitch/rhythm input, while exact score adherence, separate stems and
long-term motif retention still require testing. [Announcement](https://magenta.withgoogle.com/magenta-realtime-2),
[model card](https://github.com/magenta/magenta-realtime/blob/main/MODEL.md).

The supported real-time route uses MLX on Apple Silicon. The small model is
documented to run in real time on Apple Silicon Macs including Air models;
the larger model needs a supported Pro/Max device. JAX CPU and Linux CUDA/TPU
routes are documented for offline/batch/research use, not proof of Windows live
performance. Code is Apache 2.0; weights are CC-BY 4.0 with stated use terms.
**Disposition:** a valuable comparison if suitable hardware is already available;
no hardware purchase is recommended. The dated [local machine assessment](local-development-readiness.md#hardware-and-installed-software)
does not qualify this route. [Installation](https://magenta.github.io/magenta-realtime/installation.html),
[hardware table](https://magenta.github.io/magenta-realtime/models.html),
[model terms](https://github.com/magenta/magenta-realtime/blob/main/MODEL.md).

### Other generated-song services

| Candidate | Current primary-source finding | Disposition |
| --- | --- | --- |
| Lyria Clip / 3.5 | Supplied lyrics, singer descriptions, structure, key and BPM can be prompted. Clip always produces 30 seconds; 3.5 targets longer songs. The guide states single-turn generation and no iterative clip editing. [Music guide](https://ai.google.dev/gemini-api/docs/music-generation) | Useful vocal-quality or anticipated-section comparison. No documented ongoing intervention mechanism was established. |
| MiniMax Music API | Documents lyrics, structural tags, reference covers and streamed output, but closes paid Music/Lyrics APIs to new users from 20 August 2026. [API notice](https://platform.minimax.io/docs/api-reference/music-generation) | Not available under the project's assumed new-account route; older price/model rows do not override the notice. |
| MiniMax open Music3 | CUDA-based song generation; model card states non-streaming inference. Reduced-memory offloading is slower, and musical prompts are not strict symbolic guarantees. [Model card](https://huggingface.co/MiniMaxAI/MiniMax-Music3) | Does not remove the current hardware or live-control problem. No local benchmark or suitable deployment licence has been established here. |
| Suno | A first-party portal advertises a REST API for songs, covers and mashups, then requires sign-in. Public endpoint contracts, admission, prices, latency, stream controls and output-use terms were not established. [Official platform](https://platform.suno.com/) | Retain for official contract discovery if it can answer a surviving gap. A blanket statement that Suno has no official API would be wrong; unofficial wrappers remain unqualified. |
| Udio | Official help says there is no public API. [API status](https://help.udio.com/en/articles/10756277-udio-public-api) | No qualified programmatic route. Do not substitute an unofficial wrapper or an unmeasured latency assertion. |

Google lists Clip at $0.04/song and 3.5 at $0.08/song, without free API tiers.
RealTime is absent from the reviewed pricing table, so its tariff remains
unresolved. New paid-tier onboarding generally requires at least $5 prepaid
credit and billing setup; actual eligibility, quota and session limits need
account verification. The Gemini consumer subscription is a separate product.
[Pricing](https://ai.google.dev/gemini-api/docs/pricing),
[billing](https://ai.google.dev/gemini-api/docs/billing),
[project rate limits](https://ai.google.dev/gemini-api/docs/rate-limits).
For later distribution, Gemini API terms require Paid Services for clients
available in the UK and exclude clients directed towards or likely to be
accessed by under-18s. That may materially constrain this game's eventual
audience; it does not settle the audience now. [API terms](https://ai.google.dev/gemini-api/terms).

### Precisely controlled singing and local music

| Candidate | What is actually controllable | Remaining boundary |
| --- | --- | --- |
| Synthesizer V Studio 2 | Editor scripting can set MIDI pitch, onset, duration, lyrics and phonemes, with selectable voice databases. [Note API](https://resource.dreamtonics.com/scripting/Note.html) | JavaScript/Lua editor automation is not a documented headless, hosted or redistributable game API. [Scripting scope](https://resource.dreamtonics.com/scripting/) |
| Synthesizer V Engine SDK | Dreamtonics lists an SDK for business licensing. [Business offering](https://dreamtonics.com/contact/) | A real qualification lead. Public deployment targets, streaming, cancellation, concurrency, pricing and response-time contract remain unknown. |
| VOCALOID6 / VOCALOID:AI | Editor accepts melody and lyrics, voice choice and expression; standalone/VST3/AU operation with MIDI input and WAV output. [Features](https://www.vocaloid.com/en/vocaloid6/), [specifications](https://www.vocaloid.com/en/vocaloid6/specs/) | Yamaha's research first processes the entire score, then renders frames with expressive changes. It does not establish live replacement of arbitrary lyrics/notes. A historic Unity SDK is not current Godot/runtime availability. [Technical explanation](https://www.yamaha.com/en/tech-design/research/technologies/aisynth/), [2015 SDK announcement](https://archive.yamaha.com/ja/news_release/2015/15122101.html), [current business route](https://www.vocaloid.com/business/) |
| Soundpipe | Embeddable C DSP, oscillators, effects and sample-accurate processing; MIT licence. [Repository and status](https://github.com/PaulBatchelor/Soundpipe), [licence](https://github.com/PaulBatchelor/Soundpipe/blob/master/LICENSE) | Sound rendering, not a composer or singer. The repository is archived; integration and maintenance need assessment. |
| Pure Data / libpd | Host-controlled DSP, MIDI/control messages and audio-buffer processing through an embeddable library. [API](https://github.com/libpd/libpd/wiki/libpd), [project](https://github.com/libpd/libpd) | Viable accompaniment mechanism; compositions, singing and a Godot bridge remain separate work. |
| Tone.js | Browser synthesis/sampling with musical transport, note scheduling, tempo changes and cancellation. [Project](https://github.com/Tonejs/Tone.js), [transport implementation](https://raw.githubusercontent.com/Tonejs/Tone.js/dev/Tone/core/clock/Transport.ts) | Useful browser comparator; not a native Godot singing engine. |
| Symbolic Magenta | MusicRNN can continue a quantised NoteSequence; suitable checkpoints accept chord conditioning. [Implementation](https://github.com/magenta/magenta-js/blob/master/music/src/music_rnn/model.ts) | Inspectable note-generation comparator, with musical quality and timing unmeasured. The archived Python project, Magenta.js and MRT2 are distinct. [Python status](https://github.com/magenta/magenta), [Magenta.js](https://github.com/magenta/magenta-js) |

The unlinked **Csonic** name in MusicalRPG 2 was not identified as a relevant
music framework in the bounded search. It is unresolved, not silently substituted
with Csound.

Synthesizer V's $99 Studio 2 Pro editor with one voice, and $79 additional
Dreamtonics voices, are production-authoring prices. Its listed Windows minimum
does not require a dedicated GPU. Neither this nor advertised fast rendering
qualifies concurrent game use or new-lyric latency. [Product specifications and pricing](https://dreamtonics.com/synthesizerv/).
The editor EULA requires contact for commercial embedding and restricts use by
unlicensed others. Voice database terms separately constrain embedding and using
rendered singing as input to another synthesis model or application. Therefore
a Synthesizer V guide-vocal-to-Voice-Changer pipeline is **not an already cleared
combination**. SDK and voice rights must cover the actual deployment and any
conversion step. No enquiry was sent. [Studio EULA](https://dreamtonics.com/wp-content/uploads/2025/05/SynthesizerVStudio2ProEULA_EN.txt),
[voice database EULA](https://dreamtonics.com/wp-content/uploads/2025/02/SynthesizerV_VDB_EULA_ALL.txt),
[terms index](https://dreamtonics.com/terms/).

### Scene and lyric direction

The original OpenAI, Groq, Together AI, Llama and Mistral suggestions belong here,
not in the singing layer. Their useful output is a proposed intention, valid
world references, metered words and musical instructions for a renderer.

OpenAI documents schema-constrained output and streaming, while warning that
structured results can still contain mistakes, refusals or incomplete responses.
Together also provides schema output on supported models. These interfaces can
constrain a performance plan's shape, not guarantee musical correctness or truth
about game state. [OpenAI structured outputs](https://developers.openai.com/api/docs/guides/structured-outputs),
[Together structured outputs](https://docs.together.ai/docs/inference/chat/structured-outputs).
The game must still check who is present, what happened, the singer's range,
syllable budget and timing before accepting a proposal. Partial streamed JSON
is not automatically a valid performance instruction.

Groq's strict schema mode supports selected models, but its current guide says
Structured Outputs cannot be combined with streaming or tool use. JSON object
mode is a weaker format guarantee. The archived `llama3-8b-8192` example was
retired on 30 August 2025. Its quoted token speed and 100–250 ms verse estimate
do not establish current whole-plan latency, metrical quality or audible singing.
[Groq structured outputs](https://console.groq.com/docs/structured-outputs),
[deprecations](https://console.groq.com/docs/deprecations).

The assertion that all local models are impossible without a discrete GPU is
also too broad: llama.cpp documents x86 CPU inference, quantisation and Vulkan/
SYCL support. A small supported Llama/Mistral-family text model is a possible
later comparator, conditional on its licence, actual memory use and contention
with the game. No text model was installed or benchmarked. [Primary runtime documentation](https://github.com/ggml-org/llama.cpp).
Choose a current model only when an approved runtime lyric experiment needs one;
there is no evidence yet to select a permanent provider or buy a second account.
Development-agent usage does not fund runtime APIs; the existing
[dependency owner](dependency-options.md#generated-sung-contributions) records
that boundary.

### Scheduling and mixing

Godot documents beat/bar/end transitions, synchronised streams and generated
PCM playback. The locally qualified setup can serve as their initial measurement
platform for rendered phrases and controllable accompaniment. These features
schedule supplied music; they do not create compatible harmonies or singing.
Incremental decoding, common sample rate, buffering, reliable clocks and
underrun handling still need qualification. [Existing Godot assessment](godot-fit-assessment.md#musical-responsiveness),
[audio synchronisation](https://docs.godotengine.org/en/stable/tutorials/audio/sync_with_audio.html).

Wwise adds musical authoring and stingers; its SDK exposes sample-offset MIDI
scheduling and stopping. FMOD supplies quantised instruments, transition regions
and runtime PCM/programmer sounds. Both can respond during playback using
prepared material, contrary to the archive's absolute claim that pre-rendered
audio cannot adapt. Neither invents a new event-specific sung contribution or
repairs incompatible note content. [Wwise MIDI SDK](https://www.audiokinetic.com/library/2024.1.6_8842/?id=namespace_a_k_1_1_sound_engine_ab24b5dc8bd4d1adbdc6aa5c98d94d946.html&source=SDK),
[FMOD instruments](https://www.fmod.com/docs/2.03/studio/working-with-instruments.html),
[FMOD runtime PCM](https://www.fmod.com/docs/2.03/api/loading-and-playing-sounds-in-the-core-api.html).

Godot integration would add community bindings whose version compatibility and
MIDI/PCM feature coverage need proving. FMOD explicitly states it has no official
Godot integration. [Wwise Godot binding](https://github.com/alessandrofama/wwise-godot-integration),
[FMOD Godot guidance](https://ggj.fmod.com/docs/Development/Godot/working-with-godot.html).
Their free commercial tiers are conditional: Wwise lists Indie core licensing
up to a $250,000 production budget; FMOD lists a budget below $600,000 plus
developer annual gross revenue/funding below $200,000, registration and attribution. Do not
assume eligibility or included premium plug-ins. [Wwise pricing](https://www.audiokinetic.com/pricing/for-games/?asia=),
[FMOD licensing](https://www.fmod.com/licensing), [FMOD terms](https://www.fmod.com/legal).
**Disposition:** add neither before the native baseline exposes a need.

## Combinations worth testing

These comparisons are engineering inferences from the preceding contracts.

| Route | What it could achieve | Main failure that would reject or narrow it |
| --- | --- | --- |
| ElevenLabs contextual whole-mix continuation + Godot | New sung material carrying context from the previous performance, scheduled at a phrase boundary; fewest new dependencies on this machine. | New material arrives too late, loses motif/harmony, restarts the song or cannot distinguish participants. Success qualifies bounded phrase adaptation, not live editing of the audible phrase. |
| Shared score + local accompaniment + ElevenLabs a cappella/conditioned singing | Local control of the ongoing bed, with freshly generated vocal contributions. Test the provider's favourable layering claims directly. | Vocals miss the actual chord/beat/melody, include unwanted backing, or need excessive editing/stem processing. Matching key/BPM alone is insufficient. |
| Shared score + local accompaniment + licensed score-driven singer | Explicit note, timing, lyric and voice allocation offers the strongest control mechanism, including different participants. | No usable runtime SDK/licence, inadequate English singing, excessive response time or CPU contention. Editor playback alone cannot pass. |
| Lyria RealTime + separate singing | Responsive instrumental texture with newly generated vocals. | Independent systems disagree about chord progression or phrase shape; resets break transitions; buffering erases apparent control latency. |
| MRT2 + explicit MIDI plan + separate singing | More direct generative pitch/rhythm control than Lyria's prompt/configuration interface. | Supported hardware unavailable, pitch commands not followed reliably, short context loses form, or the singing gap persists. |

One small proposed musical state shared by the candidate components would retain
the current harmony and beat/phrase position, original motif, dramatic aim,
participants and pending changes. It would allow new composition while keeping
the already-heard performance as context. This is a hypothesis to test, not a
new domain schema or adoption of the archived six-system design.

The synchronization burden is material. A score-driven accompaniment cannot
guess the harmony inside a newly generated full mix. A streamed generator may
buffer future audio before an event arrives. A vocal can be decoded and still
miss the next useful phrase entry. Request cancellation, output discard and
stopping an audible character are three different operations. In particular,
walking away may only change audibility: the guard's valid performance can
continue in the world. Invalidate pending material when its facts, purpose or
participants become obsolete, not merely when the listener moves.

## Phased assessment plan

Each phase should answer one selection question before funding the next. The
following are proposed experiments; this report has not implemented or run them.
Use original material and retain every attempted outcome, including late or
failed responses. Numerical latency targets should follow producer judgement
of the actual musical opportunity, as required by issue #1.

### Phase 0 — make the first comparison executable

**Question:** can a contextual test be run through the existing account without
a new purchase, broader key authority or an assumed reusable reference?

The public-contract review is complete. A targeted local read also verified that
all three trial requests set `store_for_inpainting=false`; Take 3's completion
contains a song ID. Neither fact establishes retained reference availability.
The [trial owner](music-provider-assessment.md#measured-results) records this
finding. With applicable account access, verify the narrow Music endpoint
entitlements, existing allowance, metering for uploaded and retained duration,
and any safe read-only way to establish source retention. Do not send a compose
request as a supposedly free access check. If reuse is unverified, price the
documented upload route explicitly.

Prepare the exact request bodies, chosen source range, lyric variants and
measurement runner for review. No listening result arises from this phase;
its pass is a reviewable experiment with a usable source path and bounded cost.
If entitlements or billing cannot be reconciled, pause that candidate and resolve
the specific uncertainty. No upload, new render or widened key scope is implied.

There is no `scratch/` in this worktree. Any later disposable runner/capture must
use an authorised existing project-root scratch location under `AGENTS.md`;
do not silently create another temporary store. The report itself needs none.

### Phase 1 — falsify contextual singing before adding services

**Question:** can ElevenLabs carry a performance through two new events while
preserving its musical identity and reaching a useful entry?

Use the saved Take 3 as the starting performance, with its actual musical ending
auditioned and measured first. A fixed source and supplied test lyrics isolate
contextual audio generation from runtime lyric generation. They do not qualify
the latter. Do not assume the take obeys the original C-major/120-BPM prompt.

1. While the source plays, introduce an unanticipated player intention, such as
   helping recover the apples. At that moment submit one retained-source plan
   with the source's selected 12-second range followed by a new 12-second sung
   response. Keep context adherence high and request preservation of the heard
   motif and musical character. Store the result for the next operation.
2. While its usable continuation plays, introduce an NPC-initiated change, such
   as the guard choosing to help when another apple escapes. Submit a second
   plan retaining the preceding new 12-second section and generating the next
   12 seconds. Keep the same lead singer for this first discrimination; a second
   singer is tested separately below.
3. Record request dispatch and all arrivals, identify the first **new** sung
   material, and attempt each entry in sequence. Do not count re-emitted prefix
   audio as a responsive answer or replay that prefix at the seam. If the chosen
   runtime entry is missed, retain an offline seam audition as separate evidence:
   it can distinguish slow generation from failed composition.

Judge all five dimensions across the complete chain. The producer should hear
the first audition without subtitles, then verify words and event relevance.
Analyse actual tempo/beat phase, harmonic movement, motif and transition positions
where tractable; ambiguous estimates need listening, not invented precision.
Compare with the saved-take integration baseline without attributing synthetic
waits to the provider.

**Proposed new envelope:** at most one upload of 12 seconds of existing audio
and two composition requests, each producing at most 24 seconds including its
retained prefix; no automatic retries, other endpoints or purchases. At the
published $0.15/minute rate, charging all 60 submitted/output seconds would be
about **$0.15** before tax; new-material-only charging would be lower. Actual
inpainting/upload metering is unresolved, so this is an estimate, not a quote.
Propose a fresh **$1 maximum displayed debit from existing included allowance**,
checked after each operation, with adequate remaining headroom before the next.
Timeouts count as attempts. If an individual charge cannot be bounded or verified,
stop. Renewal and automatic top-ups remain off. This proposal is **not** an
extension of the exhausted three-request approval.

**Proceed** if both successive responses are intelligible, refer to their events,
retain the performance's musical identity and arrive within opportunities the
producer finds convincing. This establishes feasibility for that chain only.
**Narrow or reject** the route if a good offline seam arrives too late, the second
adaptation drifts away, or keeping context prevents the lyric from changing.
A runtime failure with successful offline composition may still support anticipated
sections; record that narrower use explicitly rather than calling it live success.

### Phase 2 — discriminate the remaining control and singing gaps

**Question:** which component must change if contextual whole-mix rendering
cannot meet the broader brief? Select the relevant branch from Phase 1's failure;
do not purchase every candidate.

| Branch | Smallest discriminating experiment | Prerequisites, cost and proceed/reject condition |
| --- | --- | --- |
| Independent singing over controlled accompaniment | Generate two new intentions against one original melody/harmonic plan and common clock. First try ElevenLabs a cappella/conditioning, then only if justified an approved stem route. Require correct lyric stress, entry, chord fit and recognisable motif. | Each Music call is newly priced/authorised; stem cost and access must be verified separately. Proceed only if the vocal works in the bed without repairing it by substituting a whole mix. Separation is not assumed to reduce response time. |
| Exact score-driven singing | Qualify Synthesizer V Engine SDK and Yamaha's current runtime offering, then render two English intentions onto the same short melody, including a second character's compatible part. Replace an unrendered phrase and suppress a superseded result. | First gate is the actual SDK/runtime/voice licence and deployment contract, not an editor purchase. No vendor enquiry is authorised here. SDK price and trial access are unknown; require a concrete offer before spending. A runtime that renders newly supplied complete phrases can pass; pre-authored-only or editor-only playback cannot establish the required runtime use. |
| Continuous generative accompaniment | Compare a simple local note-controlled bed with Lyria RealTime at fixed tempo/scale. If supported hardware is available, compare MRT2 using the same original MIDI motif. Introduce new orchestration, repeat the motif and test tempo/key changes separately. | Local baseline can avoid service charges; additional DSP installations remain implementation work. Lyria account tariff/quotas require verification; MRT2 hardware and licence need qualification. Proceed only if gains in musical quality survive the same timing and coherence tests. |
| Repeated voice identity | Only if composition/timing pass but singer identity fails, compare an entitled Music finetune or a permitted Voice Changer route with unchanged lyric/score conditions. | Price training, source preparation and every render/conversion; finetune headline is $1.50 but account eligibility is unresolved. Check source/voice rights. Reject if identity improves at the cost of unacceptable timing or melody. |

A vendor qualification request should ask for exact note/onset/duration/phoneme
and English lyric input; incremental changes during rendering; first usable audio
and warm/cold rendering evidence; two simultaneous voices; cancellation and billing;
Windows/server/headless deployment; game redistribution or hosted service rights;
voice-database and conversion permissions; SDK evaluation access and full charges.
An answer consisting only of an editor demo does not establish the runtime need.
In-flight note/lyric replacement is valuable but is not mandatory if a new short
phrase can be rendered and scheduled in time. Reliable suppression of obsolete
output can satisfy playback validity without server-side cancellation; record
the remaining computation and billing separately.

For accompaniment, keep a local symbolic note/clock trace as the control. It can
expose timing and harmonic defects without pretending to solve natural singing.
This local comparison tests the archived procedural idea and may be done without
an audio-provider purchase once implementation location and scope are agreed.

### Phase 3 — repeated adaptation in one evolving scene

**Question:** does the leading combination keep a complete performance coherent
when events accumulate, including events that were not known at generation time?

Use one small scene and the same event sequence for the surviving routes:

| Event | Discriminating observation |
| --- | --- |
| An expected NPC entrance and planned section change | Establishes the easy planned-transition control before surprising the system. |
| Player input at varied points in a phrase | Immediate world reaction; newly relevant sung material at the next convincing opportunity; no forced restart. |
| An NPC acts independently and a second singer joins | Musical and semantic response to the NPC's action, with a distinct, compatible part rather than a generic chorus. Test simultaneous harmony as well as call-and-response. |
| A dynamic scene element changes the situation | The next lyric/compositional response reflects what actually changed; accompaniment develops accordingly. |
| The player reverses an intention while a response is pending | The superseded future contribution never leaks into playback or changes the outcome; still-valid current music can continue. |
| Deliberate modulation or tempo/metre change | Harmonic preparation, rhythmic handover and phrase form survive; a provider reset is measured and heard. |
| A reprise after more than 30 seconds and several adaptations | Original motif and dramatic consequence remain recognisable beyond both ElevenLabs' short reference and MRT2's stated receptive field. |
| Departure, return and a genuinely invalidated performer | Valid world music recedes with distance and can continue; genuinely obsolete contributions are cancelled. Returning does not resurrect an invalid request. |

Run three complete chains with varied event offsets and different intentions,
retaining all results. This is an initial repeatability check, not a statistical
reliability claim. Include an event that the rendering request could not have
predicted; a set of prefetched branches alone cannot pass responsive generation.
Budget this phase only after Phase 2 fixes the actual endpoints and maximum call
count; include uploads, discarded work, voices and service time, not just the
music that survives. No unrestricted soak test or automatic retry is proposed.

Use a single monotonic event timeline plus audio sample positions. Record:

- Event, visible acknowledgement, accepted plan, request/control dispatch,
  first packet, first decodable new audio, first relevant sung word and actual
  audible transition; distinguish local command timing from speaker timing.
- Available musical lead and added scheduling/buffer delay, drift, underruns,
  malformed/missing results, stale-output suppression and recovery after loss
  of the generator connection. Transport abort is not proof of cancelled billing.
- Local CPU/memory while the rendered scene runs, and total metered cost per
  chain, including unused work. Compare cold and warm starts separately.
- The producer's judgement on each coherence dimension, intelligibility, singer
  identity, agency and desire to try another approach, with failures timestamped.

For timing, ask whether new material becomes usable **before the selected useful
entry**, and whether waiting remains dramatically convincing. An action's audible
effect includes planning, rendering, decoding, buffering, musical scheduling and
device output. Overlap can reduce the total, so do not blindly add independently
measured durations. No universal pass threshold follows from speech latency,
the old four-second fixture, or the length of an output chunk.

**Proceed** only when the producer accepts the complete chains and the logs
support correct validity, timing and measured operation. If a dimension fails,
state which one and whether the route can meet a narrower approved use. Distinct
trade-offs need producer judgement; do not turn them into a weighted average
that conceals a missing sung contribution or harmonic failure.

### Phase 4 — select from playable evidence

**Question:** does the surviving combination realise the first playable brief,
and is its operational cost and complexity justified?

Integrate the winning audio experiment into the small encounter: player action,
event-specific music, generated player intention, NPC response and meaningful
consequence, followed by a reprise reflecting that consequence. Repeat with a
different intention. Use the established Godot build–run–observe–revise loop;
retain entertaining staging imperfections that do not break play. Judge game
appeal and how much intervention Astra required separately, as issue #1 specifies.

Only then recommend a provider/toolchain selection, supported by actual coherence,
delay, failure recovery, cost per encounter and needed human intervention.
Resolve output distribution, audience, credential hosting and service terms before
the corresponding release step; local trial rights are insufficient evidence.
Update the narrowest existing owner if a decision is accepted. No architecture
ADR is justified merely by this research recommendation.

## Recommended next action

Prepare Phase 1's exact contextual-continuation test after the Phase 0 account,
source-retention and charging checks, then obtain fresh approval for its bounded
paid operations. This is the earliest affordable test on the existing setup that
can disprove successive adaptive singing rather than repeat an isolated audition.
Keep the score-driven singer qualification alongside it as the route to stronger
control if the prompt-based system cannot meet the five coherence requirements.
