# Music-provider assessment

Reviewed against primary sources on 12 September 2026. This note supports the
first sung-response trial described by the [agreed encounter brief](https://github.com/vince-hardwick/MusicalRPG/issues/1)
and the [dependency assessment](dependency-options.md). The producer approved the
bounded trial below; this does not adopt a permanent provider. All three approved
generation requests succeeded. The producer found the words clear and delivery
acceptable in all three, preferring Take 3. Complete audio decoded in 2.78–9.76
seconds. The Godot encounter assessment is a useful basic integration exercise:
the producer accepted entry into the recording, found the longer wait stalled,
and found cut-in/departure too abrupt. The shorter wait was closer to responsive
enough, not an established latency pass. Starter access and the restricted key
are verified, renewal is cancelled at the end of the paid period, and automatic
top-ups are off. Results,
account-access status and the authorised password-change deferral are below.
The [next assessment](#adaptive-music-capability-assessment) addresses the broader
adaptive-music requirements; the initial shortlist qualified only a short reply.

## First-trial recommendation and scope

Start with **ElevenLabs Music**, using its current `music_v2_5` model, one explicit
composition chunk and original lyrics. Its documented three-second minimum,
chunk durations and detailed audio stream fit a short in-character reply more
directly than Lyria Clip's fixed 30-second output. Music v2.5 supports the same
composition, reference and inpainting workflows as `music_v2`; the provider
claims better audio quality and prompt adherence, not a measured latency
advantage. Pin the model ID explicitly. This is a reason to test it, not evidence
that it will meet the game's responsiveness needs. [Music capabilities](https://elevenlabs.io/docs/overview/capabilities/music),
[composition plans](https://elevenlabs.io/docs/eleven-api/guides/how-to/music/composition-plans).

The target is an event-specific **sung contribution**. ElevenLabs calls the
combined singing-and-accompaniment capability Music Generation. This trial does
not qualify an isolated singing voice over independently controlled accompaniment;
that distinction matters for later musical continuity and character identity.

For a new individual account, the clearer starting option is the **$6/month
ElevenAPI Starter subscription**, subject to the actual checkout price and
eligibility. A $5 PAYG top-up can unlock the Music API without a subscription,
but its underlying free plan remains unchanged while the commercial-rights
table and API-access table still describe Free and paid tiers separately.
Saving $1 is not a useful reason to leave the trial outputs' download and reuse
rights ambiguous. Starter is sufficient for a local individual assessment;
it is not blanket clearance for every future game release. No extra top-up is
needed while the included allowance suffices. [API pricing](https://elevenlabs.io/pricing/api),
[PAYG documentation](https://elevenlabs.io/docs/overview/administration/pay-as-you-go),
[model-specific terms](https://elevenlabs.io/eleven-music-model-specific-terms).

Retain **Lyria 3 Clip** as the comparison candidate if ElevenLabs fails lyric
delivery or musical quality. Do not buy two accounts before the first result
shows a reason for comparison. The [approved trial](#first-trial) below sets out
the sample, measurements and authorised spending boundary.

## Shortlist

| Candidate | Verified fit | Entry cost and disposition |
| --- | --- | --- |
| ElevenLabs `music_v2_5`; `music_v2` remains available | Explicit lyrics and 3–120 second chunks; raw audio and detailed SSE streaming; audio conditioning and inpainting. | Starter advertised at $6/month; $0.15/minute headline API rate. Preferred first trial, with billing granularity unresolved. |
| Google `lyria-3-clip-preview` | Custom lyrics in the prompt; always 30 seconds; complete audio response demonstrated. | $0.04 per song, no free API tier; new-account prepay minimum $5. Useful quality comparison, weaker duration fit. |
| Google `lyria-3.5` | Custom lyrics, larger song structure, prompt-influenced duration of a couple of minutes. | $0.08 per song, no free API tier. Excess scope for the first brief reply. |
| Google `models/lyria-realtime-exp` | Continuous steering over a bidirectional stream, explicitly instrumental only. | Cannot satisfy the sung-response requirement by itself; defer accompaniment assessment. |
| MiniMax Music API | Direct API documents lyrics and streaming, but closes paid Music/Lyrics APIs to new users from 20 August 2026. | Not available for this assumed new-account trial; no account purchase recommended. |

Sources: [ElevenLabs detailed stream](https://elevenlabs.io/docs/api-reference/music/compose-detailed-stream),
[ElevenLabs pricing](https://elevenlabs.io/pricing/api),
[Google music guide](https://ai.google.dev/gemini-api/docs/music-generation),
[Google pricing](https://ai.google.dev/gemini-api/docs/pricing),
[Google billing](https://ai.google.dev/gemini-api/docs/billing),
[Lyria RealTime](https://ai.google.dev/gemini-api/docs/realtime-music-generation),
[MiniMax API notice](https://platform.minimax.io/docs/api-reference/music-generation).

## ElevenLabs contract and limits

`POST https://api.elevenlabs.io/v1/music` composes audio;
`POST https://api.elevenlabs.io/v1/music/detailed/stream` returns server-sent
events containing composition information, metadata, audio chunks and completion,
with optional word timestamps. The reference accepts `music_v1`, `music_v2` and
`music_v2_5`; its documented default is still `music_v1`. A client must not rely
on that default. `prompt` and `composition_plan` are mutually exclusive, and
`music_length_ms` is for prompt requests. With a plan, supply the duration in
each chunk instead. The v2-family automatic format is documented as
`mp3_48000_192`; other MP3 and PCM formats are listed. Verify any format-specific
plan entitlement before requesting it. [Compose endpoint](https://elevenlabs.io/docs/api-reference/music/compose),
[detailed stream endpoint](https://elevenlabs.io/docs/api-reference/music/compose-detailed-stream).

A v2-family composition plan contains ordered `chunks`, each with `text`,
`duration_ms` and `positive_styles`, plus optional negative styles and context
adherence. A single 12-second chunk is within the documented limits. Put the
original lyric lines in `text`, separate from broad vocal and accompaniment
directions. The chunk guide allows 3–120 seconds per chunk, up to 30 chunks and
3–600 seconds total. The general overview still says five minutes maximum;
that inconsistency does not affect this short trial. The three-second minimum
is an **output-duration limit**, not a claim about first-audio delay or a
minimum billable unit. [Composition guide](https://elevenlabs.io/docs/eleven-api/guides/how-to/music/composition-plans),
[general overview](https://elevenlabs.io/docs/overview/capabilities/music).

Streaming transport is useful but insufficient evidence of responsiveness.
The official streaming cookbook actually collects the entire response before
calling its playback helper. It therefore cannot serve as a first-playable-audio
benchmark. No numeric first-sung-word guarantee was found in the reviewed Music
contract or guide. Measure network arrival, decodability, the first usable sung
word and full completion separately. The much lower latency figures advertised
for ElevenLabs speech models do not describe Music. [Streaming example](https://elevenlabs.io/docs/eleven-api/guides/how-to/music/streaming),
[API model pricing and descriptions](https://elevenlabs.io/pricing/api).

For continuity, stored songs can supply unchanged audio chunks or a conditioning
reference of at most 30 seconds. Conditioning strength influences similarity;
it does not promise a fixed singing identity. The music request has no ordinary
TTS `voice_id` field. A seed may improve consistency but does not guarantee
reproducibility. Music finetunes exist and mention vocal character, but require
additional data, processing and cost. Reference reuse, finetuning and repeated
character identity are follow-on questions after one usable sung response.
[Inpainting and conditioning](https://elevenlabs.io/docs/eleven-api/guides/how-to/music/inpainting),
[request schema](https://elevenlabs.io/docs/api-reference/music/compose-detailed-stream),
[finetune overview](https://elevenlabs.io/docs/overview/capabilities/music).

### Published billing and uncertainties

The current ElevenAPI page lists Music at **$0.15 per minute**, Starter at
**$6/month**, and 40 included Music minutes for that plan. It says API billing
uses dollars rather than credits, but also says Music is metered per generation.
It does not clearly specify short-generation rounding, a billing minimum, or
charges after an interrupted stream. Three 12-second outputs have a headline
duration-based value of **$0.09**; this is arithmetic, not a confirmed charge.
The subscription is the actual entry purchase, and unused allowance is not a
cash saving. The pricing page excludes taxes; confirm the final checkout amount
rather than treating $6 as a UK tax-inclusive quote. [API pricing and FAQ](https://elevenlabs.io/pricing/api).

PAYG requires at least **$5**, is prepaid, is non-refundable and expires after
12 months. Automatic top-ups are optional. Its FAQ explicitly says it unlocks
Music on a free account, despite the Music quickstart's older blanket paid-user
wording. Do not infer paid-plan output rights from API access alone. The
model-specific terms also show generation allowances differing from the newer
API pricing page. Preserve the selected account's actual allowance and tariff
in trial evidence; do not silently substitute the creative website's credit
economy. [PAYG](https://elevenlabs.io/docs/overview/administration/pay-as-you-go),
[quickstart](https://elevenlabs.io/docs/eleven-api/guides/cookbooks/music),
[rights table](https://elevenlabs.io/eleven-music-model-specific-terms).

### Output use and game integration

The Music model terms cover the v1 and v2 version families. Starter through Pro
are for individuals; higher tiers have different entity eligibility. Self-serve
media rights exclude **Studio Games**, defined there as games that are monetised
and offered through more than one platform. The phrase is not defined by studio
size. Only the full Enterprise Music column grants all media rights; Enterprise
Music Lite retains the exclusion. Their separate **Streaming Rights** category
means third-party music streaming platforms, not receiving an HTTP audio stream.
Self-serve plans also prohibit music libraries/repositories intended to make
outputs available to third parties. That does not establish that every source
repository containing a game asset is prohibited. Assess the actual distribution
and asset reuse terms before publishing generated audio; the first local trial
does not require that publication. [Model-specific terms](https://elevenlabs.io/eleven-music-model-specific-terms).

Music API terms expressly contemplate enhanced applications, require confidential
credentials and an appropriate API-client privacy policy, and restrict making
API access available to others without authorised-reseller status. Their reseller
definition concerns minimal added functionality or model aggregation. A substantive
RPG appears different from a thin music generator, but that is an inference, not
an explicit written clearance for our final design. Recheck before an end-user
release, output-library publication or monetised multiplatform release; it need
not prevent an individual local technical trial. [Music API terms](https://elevenlabs.io/music-api-terms).

Use original lyrics and descriptive musical styles. Music terms prohibit artist,
songwriter, song and album names in inputs, references intended to reproduce
existing lyrics, and misleading artist impersonation. The applicable general
terms for this UK user are the EEA/Switzerland/UK version. They do not promise
exclusive or legally protectable generated output. [Music terms](https://elevenlabs.io/music-terms),
[UK-applicable general terms](https://elevenlabs.io/terms-of-use-eu).

## Google alternative

The current guide uses `POST
https://generativelanguage.googleapis.com/v1beta/interactions` with model
`lyria-3-clip-preview` or `lyria-3.5`. Python, JavaScript and REST examples agree
on these IDs; a Java example still contains `lyria-3-generate-001`, so do not copy
that conflicting identifier. Output is 44.1 kHz stereo MP3, with WAV available
for Lyria 3.5. Custom lyrics and singer characteristics are prompt instructions.
The guide demonstrates completed audio retrieval, states single-turn generation
and no iterative editing of a generated clip, and gives no first-audio deadline.
Do not treat the Interactions API's general streaming facilities as proof of
incrementally playable Lyria vocal output. [Music guide](https://ai.google.dev/gemini-api/docs/music-generation).

Clip always produces 30 seconds at **$0.04 per song**; a shorter useful passage
does not reduce that request price. Lyria 3.5 costs **$0.08 per song** and is
oriented towards longer structures. Neither has a free API tier. New Gemini API
accounts default to prepayment with at least **$5** in credits, usable for Gemini
API charges, expiring after one year. No paid Gemini consumer subscription is
required by this developer billing route. Do not count Google Cloud welcome
credits as funding for the trial. Three Clip results would use $0.12 at the
published per-song rate, separate from the $5 entry funding. [Pricing](https://ai.google.dev/gemini-api/docs/pricing),
[billing](https://ai.google.dev/gemini-api/docs/billing).

Generated music includes SynthID, and named-artist voices and copyrighted lyric
requests are filtered. No fixed singer identity is promised. Google's API terms
also disallow API clients directed towards or likely to be accessed by under-18s
and require Paid Services for clients made available in the UK. Those boundaries
matter if this becomes a broadly accessible game; they do not decide its intended
audience here. Google does not claim ownership of generated content and does not
promise uniqueness. [Music limitations](https://ai.google.dev/gemini-api/docs/music-generation#limitations),
[Gemini API terms](https://ai.google.dev/gemini-api/terms).

Lyria RealTime (`models/lyria-realtime-exp`) is separately documented as an
experimental, continuously steerable, instrumental-only model. Its low-latency
stream cannot supply the required intelligible sung lyric. [RealTime guide](https://ai.google.dev/gemini-api/docs/realtime-music-generation).

## Bounded alternative check

MiniMax is a credible direct provider, and its Music API documents custom lyrics,
streaming and model `music-3.0`. However, both its API reference and pricing page
announce closure of paid Music/Lyrics APIs to **new users from 20 August 2026**,
while existing paying users can continue. Old model listings and price rows are
not evidence of new-account eligibility. Its website or open model would involve
a different assessment, so neither is substituted for the requested API trial.
No unofficial Suno/Udio wrapper is assumed to be an authorised provider API.
[MiniMax API](https://platform.minimax.io/docs/api-reference/music-generation),
[MiniMax pricing notice](https://platform.minimax.io/docs/guides/pricing-paygo#music).

## First trial

The producer approved this trial on 12 September 2026, including one monthly
Starter period and at most three generation attempts using up to $1 of its
included allowance. The sample is not an adopted gameplay scenario. Ask one
narrow question: can the provider turn a supplied event-specific
lyric into an intelligible, appealing short performance, and how long must we wait
for it? Supplying the lyrics isolates that question from runtime story and lyric
generation, which this trial will not qualify.

Use an earnest guard whose apples the player has tipped into a fountain. Generate
the following original 16-word reply three times with the same request:

> You tipped my apples in the fountain's spray;
>
> Now fish them out before they float away!

Request one 12-second `music_v2_5` composition chunk, a sincere, lightly comic
baritone with clear British English diction, sparse piano and pizzicato strings,
120 BPM and C major. Ask for the supplied lyrics only, with no long instrumental
introduction. These are creative directions to evaluate, not guaranteed musical
properties or settled game canon. Use three separate sequential generations,
retaining every outcome rather than choosing only the best one.

### Access and approved spending

- Purchase one monthly **ElevenAPI Starter** period at the advertised **$6**, with
  the actual currency, tax and plan entitlement confirmed at checkout. Avoid an
  annual commitment. Unavailable payment details or checkout verification still
  need the producer.
- Make at most **three generation requests**, spending at most **$1 of the
  included allowance** as an operating boundary, with no additional top-up or
  automatic retries. The nominal 36-second total is $0.09 at the published rate;
  the $1 allowance is not a predicted charge or an additional purchase.
- Before generation, record the account's displayed allowance and tariff. Check
  usage after each request; do not continue if actual metering contradicts the
  estimate or cannot be reconciled with the agreed allowance. A timeout may still
  incur a charge and counts as an attempt. This client-side limit is not a claim
  that the provider offers a matching hard cap.
- Keep automatic top-ups off. Confirm renewal handling so another subscription
  period requires a deliberate decision. The producer will create the account
  and save its login in Bitwarden. They have authorised Computer Use with
  Bitwarden autofill for this account, copying the trial API key through the
  clipboard, and saving it in a Bitwarden secure note and encrypted local state.
  Keep credentials out of chat, tracked files and the game client. Vault unlock,
  sign-in verification or unavailable payment details may still need the producer.

The [local readiness assessment](local-development-readiness.md) establishes the
available authoring and audio-observation tools. No additional engine, MCP or
plugin has emerged as a prerequisite. A disposable runner is prepared under
`scratch/music-provider-trial/`. Its PowerShell entry point defaults to a read-only
subscription check; `generate-one` sends one request and requires a reported
monthly Starter tier. It reserves attempts before sending, refuses a fourth
attempt, and has no automatic retry. It requests MP3 at 44.1 kHz/128 kbps and uses
the already-qualified SoundFile environment to decode a complete response.

Seven offline checks passed for response retention, event parsing, separation of
metadata from audio, decoding/timing, read-only account checks and refusal of a
fourth attempt. PowerShell syntax also passed. These checks used synthetic data
and a mocked account response; the separate live results are below. The
subscription API exposes legacy credit counters, so the runner does not translate
those into dollar charges or claim to enforce the $1 boundary itself. Actual
metered usage was reviewed before each subsequent generation.

The local key helper uses Windows user-bound encryption. The trial key is stored
encrypted under `scratch/music-provider-trial/`; it is excluded from Git and from
the local audition server's document root. Creation and saved-settings inspection
confirmed **Music Generation: Access** and **User: Access**, with all other endpoint
groups set to No Access. The User control has no separate Read option; the runner
uses it only for the subscription GET. The key expires on **19 September 2026**,
with auto-disable-if-leaked enabled. No provider credit quota was set because its
credit units were not yet qualified at creation; the three-attempt limit and
per-request metering review supplied the approved trial boundary. Live account
reads and all three music requests succeeded using this restricted key.
[API authentication](https://elevenlabs.io/docs/api-reference/authentication),
[API-key administration](https://elevenlabs.io/docs/overview/administration/workspaces/api-keys).

An autofill attempt submitted a credential-like clipboard value to Google through
Edge's `Ctrl+Shift+L` shortcut. Its value and the search URL are not recorded here.
The producer acknowledged the incident, explicitly authorised continuing with the
saved vault login, and deferred changing the password until later so assessment
can continue. Revisit the producer-owned password change at trial closeout; the
password remains exposed until replaced. No trial API key or paid generation was
created by the sign-in attempts. Returning to the sign-in page did not undo the
disclosure.

Do not use `Ctrl+Shift+L` in Edge for autofill: it is also Edge's **Paste and search /
Paste and go** command, and this local attempt activated that browser command.
No browser shortcut or security setting has been changed. [Edge keyboard shortcuts](https://support.microsoft.com/en-us/edge/keyboard-shortcuts-in-microsoft-edge),
[Bitwarden autofill](https://bitwarden.com/help/auto-fill-browser/).

The producer completed sign-in, checkout verification and payment. The invoice
list confirms **Paid, $7.20**; checkout had displayed the GBP option as **£4.62 plus
£0.92 VAT, £5.54 total**. The settled bank-card currency was not independently
checked. Both the authenticated UI and subscription API confirm monthly Starter.
The billing page confirms cancellation at the end of the paid period on
**12 October 2026**, with current Starter access retained, a $0 top-up balance and
**Auto Top Up Off**. The API reports credit extension disabled.

This session's browser security policy rejected access to Bitwarden's extension
page and explicitly prohibited alternative automation routes for the same vault
access. Saving the trial key in Bitwarden therefore requires the producer's
direct action. Its one-time display was left open and the key copied to the
clipboard for that handoff; vault saving has not yet been confirmed. The encrypted
local copy has been verified independently.

### Measured results

Three separate sequential requests used the same request body and produced three
different audio hashes. Each returned HTTP 200 and a 12.042-second, 44.1 kHz stereo
recording. There were no retries or parser/decoder failures. All three detailed
streams returned **one audio chunk containing the whole requested phrase**, then
composition, metadata and completion events. This run therefore establishes no
useful incremental-playback advantage from the streaming endpoint.

| Take | First complete audio event | Response complete | Decoded audio ready | WAV file ready | Provider's first-word offset | Estimated request-to-first-word wait |
| --- | ---: | ---: | ---: | ---: | ---: | ---: |
| 1 | 2.674 s | 2.676 s | 2.780 s | 2.789 s | 0.560 s | 3.349 s |
| 2 | 3.033 s | 3.040 s | 3.134 s | 3.144 s | 0.119 s | 3.263 s |
| 3 | 9.660 s | 9.662 s | 9.756 s | 9.767 s | 0.099 s | 9.866 s |

Timings use the local monotonic clock from immediately before the generation
request. They include connection setup and response processing, but exclude the
read-only subscription preflight. The first-word column comes from the returned
`words_timestamps`; it has not been independently checked by listening. The final
column adds that offset to WAV readiness and assumes immediate playback. It is
an estimate, not a measured action-to-audible-word delay in Godot. The listening
page plays saved files and does not reproduce a live generation wait.

The usage dashboard confirmed 150, 300 and finally **450 credits**, respectively,
with **three billable requests and 36 seconds** in total. Immediate subscription
reads lagged the dashboard and must not be treated as evidence of zero charge.
Each take consumed 150 credits. Relative to the advertised 30,000-credit Starter
allocation for $6, 450 credits is 1.5%, or **$0.09 of subscription value**. This
agrees with the $0.15/minute headline calculation and is below the approved $1
allowance boundary. Actual metering was in credits; this is not a separate dollar
charge or a claim that credits are refundable cash. The account began with 40,000
available credits, which is recorded separately from the advertised recurring
allocation; its extra 10,000 were not assumed to recur.

Raw streams, event arrival records, returned word timestamps, request identities,
audio hashes and decoded files are in the disposable trial directory. A local
audition page under its `audition/` child exposes only the page and three WAV files,
with requested lyrics hidden initially. Its served page and all three loaded
audio durations were visually checked. The producer's listening result is below;
independent verification of the first-word timestamps remains outstanding. The
listening feedback does not establish those precise offsets.

### Producer review and next assessment

The producer reported: "The words were clear, delivery was fine, all three were
OK. Take 3 worked best for me." This supports treating all three as acceptable
for this supplied-lyric audition, with Take 3 the preferred performance. It is
sufficient evidence to move to a contextual assessment; it does not establish
that the encounter is enjoyable to play or that character voices remain consistent
across responses.

The producer approved using saved Take 3 in a small Godot encounter assessment,
with controlled delivery delays of approximately three and ten seconds drawn
from the observed range. Using the same recording at both delays separates
judgement of the wait from preference for the performance and needs no further
generation requests. These are test conditions, not service guarantees or latency
pass marks. The implemented fixture and technical checks are below.

Assess immediate visible reaction to the player's action, continued movement and
accompaniment during the wait, entry at a musical break, and interruption or leaving
before and during the response. Check that an abandoned response does not play
later in the wrong context. This follows the agreed role-play boundary and the
qualified Godot loop. The producer's judgement during play owns whether the wait
and transition work.

The preferred take also had the longest measured generation delay, but three
samples do not establish any relationship between quality and latency. The positive
audition alone does not establish a need for another provider, but the broader
adaptive-music assessment below requires reviewing capabilities beyond this trial.

Keep raw trial captures under the existing `scratch/` directory and put the needed
measured findings in this research note. Do not depend on disposable files as the
only record of a conclusion. Public audio distribution, repeatable character
identity and runtime lyric generation remain later questions; this local audition
does not settle them.

### Godot encounter assessment

The disposable **Apples in the Fountain** fixture runs natively in Godot 4.7.2
with the qualified Compatibility renderer. It uses the original Take 3 MP3,
verified against its trial audio hash, and a locally synthesised C-major plucked
accompaniment at 120 BPM. It contains no provider credential, network request or
new generation. Its source, launcher, instructions and captures are under
`scratch/godot-encounter-assessment/`; `Launch.cmd` or `run.ps1` starts it.

Tipping the basket immediately moves the apples into the fountain and changes
the guard's visible reaction. The player remains movable while the reply waits.
After the selected delay, the response enters at the next bar of the looping
accompaniment. The accompaniment fades down during Take 3, whose generated voice
and accompaniment remain combined, then fades back after the phrase ends. This
does not qualify a separate singing stem or guarantee that the generated take's
tempo and harmony match the synthetic accompaniment. The producer's assessment
of entry and exit is recorded below.

The corrected recorded run (`sequence-b`) observed the following timing. These
are local fixture and playback-command measurements, not new provider timings
or physical action-to-speaker latency:

| Selected delivery wait | Observed delivery | Added wait for musical entry | Action to playback command |
| --- | --- | --- | --- |
| 3 seconds | 3.004–3.012 s across four deliveries | 0.984–0.997 s for the three played replies | 3.996–4.002 s |
| 10 seconds | 10.010–10.011 s across three deliveries | 1.981 s for the played reply | 11.991 s |

One short reply was interrupted while queued, and two long replies were obsolete
on delivery. They are included in the delivery counts but not the playback
columns. Selecting the next bar can add almost two seconds to a ten-second wait;
that is a behaviour for the producer to assess, not hidden generation latency.
An initial fixture run exposed early completion of a Godot timer during a slow
frame. The fixture now enforces its deadline with the monotonic clock; the table
uses the subsequent corrected run.

The same recorded sequence exercised natural completion, departure while waiting,
departure during singing, interruption while queued, and an old delivery arriving
while a newer response was singing. Request identifiers prevented obsolete
delivery from starting or replacing a current reply. Leaving faded out the
entire generated mix, including its accompaniment, over 80 ms and brought back
the synthetic bed over 120 ms; returning retained the floating apples and did
not restart the accusation. Those technical cancellation checks do not establish
perceptual musical continuity. These are narrow encounter consequences, not a
full quest or player-intention system.

The 91.99-second Master-bus recording was 48 kHz stereo, with a peak amplitude of
0.380 and no full-scale samples. Waveform matching located the saved take at the
four logged starts and supported the absence of a new opening at the checked
cancelled-delivery points; the interrupted vocal continuation was also absent
from its checked window. Three replies completed naturally and returned to the
accompaniment. This supports the audio-routing and cancellation checks; it does
not establish that the transitions sound musically convincing.

Native Computer Use separately verified button activation, delay selection with
the keyboard, an arrow-key movement during a ten-second wait, leaving during
singing, and returning (`native-input-b`). A short-tap input fix was verified by
visible movement and changed logged position. The native long case reached its
playback command at 11.992 seconds. Script checks passed and the corrected
recorded run contained no Godot error or warning lines.

The fixture controls are **1** or **2** to select a wait, **Space** to tip the
basket, arrows/WASD to move, **I** to cut in, **L** to leave, **E** to return,
**R** to reset, **M** for quiet and **Esc** to close. It bounds its Master-bus
capture to the first three minutes after the initial basket action, keeping
disposable recordings finite.

#### Producer verdict and proposed revision

The producer found the longer wait too long, resembling a stall in the action.
The short wait felt closer to responsive enough. In this fixture those cases
reached playback at roughly twelve and four seconds respectively, including
musical entry. This rejects the longer case for the current staging; it does not
establish four seconds as acceptable or set a general numerical latency target.

The transition from the melody beeps into the generated recording was OK.
Cutting in or leaving stopped the music too abruptly to feel coherent. The
producer regarded the combination of Godot and sound as a start and a basic
exercise. Accordingly, the result is a useful integration proof with unresolved
responsiveness and musical exits, not a successful playable musical encounter.

Code inspection confirms that cut-in and departure share `_stop_voice()`, which
fades the whole Take 3 mix to -80 dB in 80 ms before stopping it. Despite the
method name, this stops both singing and generated accompaniment. A resumed
synthetic bed does not by itself preserve the perceived performance. The
producer's report therefore controls the musical-continuity verdict; the earlier
recording and event checks establish only the narrower playback behaviour.

The producer accepted a focused revision using the saved take and the shorter wait
as a comparison baseline. Give a cut-in an immediate visible acknowledgement and a
short musical handover into accompaniment. Treat departure differently: let the
guard's performance continue in the world and recede as the player walks away,
consistent with ongoing role-play in the agreed brief. Recheck cancellation of
responses that are no longer valid without treating every change in listening
position as the end of the performance. This remains an unimplemented, bounded
integration revision, not adopted architecture or the main capability assessment.

Keep avoidable entry delay under review, including the extra wait for a full bar;
the provider's observed latency variation also remains unresolved. Smoother exits
would not make the long wait responsive. The proposed revision needs no new
generation or provider purchase. A full playable loop, generated player
contributions, repeatable character identity and a permanent provider choice
remain unestablished.

## Adaptive music capability assessment

The producer clarified that the project requires music generated on the fly in
response to player interactions, other characters and dynamic scene elements,
including NPC actions that may be predetermined, partly predetermined or
dynamically responsive. Harmonic, melodic, rhythmic, compositional and thematic
coherence must be assessed across both expected and responsive transitions.
Improving the fade-out of a saved recording addresses only a small integration
detail and cannot qualify those requirements.

The next work is to review the [foundational conversations](../reference/source-chats/README.md),
the [agreed brief](https://github.com/vince-hardwick/MusicalRPG/issues/1) and its
linked domain owners, then research the full relevant ElevenLabs API capabilities.
Assess whether a single provider or a combination of components can meet these
demands. Where ElevenLabs leaves gaps, investigate candidates suggested in the
original sources and prior research, verifying their current capabilities against
primary sources rather than adopting archived product or latency claims.

Produce a phased assessment plan that identifies the evidence needed to select
the best combination of tools, platforms and services. Distinguish documented
controls and guarantees, measured behaviour, provider claims and untested
possibilities. The plan should address coherent adaptation during ongoing music,
not just independent phrase generation and playback transitions. Further paid
trials remain subject to case-by-case approval; the three-request trial is complete.
