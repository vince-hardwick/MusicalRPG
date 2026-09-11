# Prompt engineering musical RPG — initial shared chat

> Orientation only. This is a source snapshot, not adopted project direction.
> See the [source index](README.md) for provenance, the Nova transcription correction and limitations.

## User — turn 1

I say, here's fun. The coming of Nova has made me think about realising a previously unrealistic project.

Here's the pitch: An Elder Scrolls RPG, but its a musical. Elaborate song and dance set pieces are performed by NPCs as you enter a settlement. Maybe there's a leading man mechanic of some sort where the player character has to sing dance as part of the set piece... TBH its so far out of reach that I can't be bothered too much with the specifics. Possible features - songs/ dances generated on the fly, potentially really badly. Really, I think there's two versions of this. One's hilarious and janky and half-finished, with generative songs and dances and things go wrong, and I think that's probably the most attractive thing, and I'm interested in doing a project like that in Nova, just getting going and seeing what happens. But it potentially forms the basis of a much more fleshed-out and good game eventually. But what I'm wondering is if we could work on prompt engineering, set of prompts that could realize something like this through Nova. I'm going to pass that on to Beacon's lead software architect, and he's going to spend a weekend seeing what Nova can do with our prompts.

## ChatGPT — turn 2

Yes. And I think the **first version should absolutely be the bad one**.

Not “bad” as in deliberately broken code, but a game whose *creative premise embraces the limitations of generative AI*: people burst inexplicably into song; choreography is suspiciously ambitious for the animation system; lyrics occasionally fail to scan; the blacksmith somehow gets a twelve-bar power ballad about municipal drainage; six villagers attempt a synchronised kick-line and one wanders into a cabbage cart. That means the prototype can succeed **because** Nova does weird things rather than only if it achieves AAA quality.

The concept I’d give your architect is something like:

> **Build a small open-world fantasy RPG in which every settlement is a musical. The player explores normally, but entering settlements, encountering important NPCs and triggering quests can cause elaborate musical numbers involving NPC singing, dancing, environmental choreography and potentially the player character. The tone should initially embrace procedural chaos, jank and unexpected emergent comedy rather than trying to achieve polish.**

And crucially, I **wouldn't give Nova one enormous “make this game” prompt**. I'd give it a hierarchy of prompts/specifications that progressively establish an architecture it can extend. That's much more likely to get you somewhere interesting over a weekend.

### The weekend experiment I'd run

The target isn't *Elder Scrolls: The Musical*. It's one **tiny vertical slice**:

**One valley → one village → pub + blacksmith + shop + 8–12 NPCs → one stupid quest → three musical numbers.**

The player can wander around in ordinary RPG fashion. Entering the village triggers the opening ensemble number. Talking to somebody starts a quest. Completing some ludicrously mundane objective triggers a finale.

For example:

**WELCOME TO DUNGLEFORD**

You walk through the gates.

A farmer starts singing about Dungleford. Another NPC joins in. Then the baker. Then the guards. NPCs move to predetermined choreography points and perform simple dance animations. The lyrics introduce places and characters that actually exist in the generated village.

Then, halfway through:

> 🎵 *Our blacksmith's name is Bernard /
>
> His ironwork is fine—*

Bernard is currently stuck behind a fence because his pathfinding has failed.

**Do not fix Bernard.**

This is important.

The first prototype should distinguish between **technical failure** and **theatrical failure**. Crashes, corrupted saves and impossible quests are bugs. Bernard missing his cue, terrible rhymes and dancers colliding are *content*.

---

I think the prompting architecture is where this gets genuinely interesting. Rather than asking Nova to continually improvise the entire game, I'd establish about six systems and get it to build them independently:

1. **RPG world system** — player movement, interaction, settlements, NPCs, dialogue, quests and inventory. Keep this intentionally primitive.

2. **Musical Director** — receives an event such as `PLAYER_ENTERS_SETTLEMENT`, examines the location/NPCs/current quests/world state and creates a structured musical-number specification.

3. **Song Generator** — turns that specification into sections, lyrics, assigned singers, timing and perhaps eventually actual generated music/vocals.

4. **Choreography Director** — assigns participating NPCs positions, gestures, animation sequences, entrances/exits and formations.

5. **Performance Controller** — actually attempts to synchronise music, lyrics, NPC animation, camera and player interaction.

6. **Chaos / recovery system** — and this one could become the secret sauce. Performances should be able to survive participants being absent, dead, obstructed, hostile, busy or physically incapable of reaching their mark.

That last system produces the proper Elder Scrolls energy. If the mayor who has the second verse was killed three hours ago, **the musical shouldn't simply throw a null-reference exception**. Somebody else gets the verse. Or there's an awkward instrumental gap. Or everyone sings his lines while staring at the empty spot where he was supposed to stand.

And suddenly your joke prototype has stumbled into something that could actually be a distinctive game mechanic.

### For the prompts

I'd actually write your architect a **prompt pack**, rather than one prompt. Something along these lines:

**Prompt 0 — Creative Constitution**

Defines what this project *is*, what Nova is allowed to change, technical principles, the comedy philosophy, and the distinction between acceptable theatrical jank and unacceptable software failure.

**Prompt 1 — Technical Director**

> Inspect the available capabilities and choose the simplest architecture capable of producing the vertical slice. Do not build systems merely because a conventional RPG would contain them. Every system must support something observable in the prototype.

**Prompt 2 — Build the Boring RPG**

> Produce the smallest functional first-person/third-person fantasy RPG environment containing one settlement, interactable NPCs, buildings, dialogue and a single quest. Use placeholders aggressively. Do not implement musical functionality yet.

**Prompt 3 — Build the Musical Event Model**

Define something structured like:

```
MusicalNumber
  Trigger
  Theme
  Participants[]
  Sections[]
  Lyrics[]
  LeadSinger
  Chorus
  Choreography[]
  PlayerRole
  StartConditions
  RecoveryRules
```

This is important because **the LLM improvises the specification, not the execution machinery**. That's how you stop the whole thing becoming an uncontrollable soup.

**Prompt 4 — Make Dungleford Sing**

> When the player enters the settlement for the first time, create a musical number involving available NPCs. The number should introduce the settlement and at least three important NPCs. Characters must sing about facts that are true of the current world state. Generate choreography using only supported movements and animations. Execute the resulting MusicalNumber through the performance system.

Then iterate.

**Prompt 5 — Break It**

This might be the most entertaining prompt of the lot:

> Systematically create situations that would disrupt the Dungleford musical: obstruct performers, remove performers, initiate dialogue during the number, move the player somewhere unexpected, kill or disable a required NPC, trigger combat, and create pathfinding failures. Make the performance system recover wherever possible rather than restarting or crashing. Preserve amusing imperfect outcomes where they do not prevent gameplay.

Then you see what survives.

There's a serious prompt-engineering principle behind that structure too: current Nova guidance explicitly recommends breaking complex agentic work into stages, providing clear tool/orchestration rules and examples rather than relying on one giant ambiguous instruction. [AWS Documentation +2](https://docs.aws.amazon.com/nova/latest/nova2-userguide/building-ai-agents.html?utm_source=chatgpt.com)

And I think there's an even better idea hiding inside your “leading man mechanic”.

Don't make the player **actually sing** initially. Give them **musical RPG dialogue choices**:

> 🎵 *“I WILL SAVE YOUR DAUGHTER!”*
>
> 🎵 *“WHAT'S THE REWARD?”*
>
> 🎵 *“I'M AFRAID OF SPIDERS!”*

Selecting one inserts the protagonist's line into the number and determines what everyone else sings next.

Later, *then* you get ridiculous: microphone input, pitch detection, rhythm, dance/QTE controls, deliberately forgiving scoring, NPC reactions to catastrophically poor performances, Bard skill tree, etc.

But none of that belongs in Weekend One.

The success criterion I'd give your architect is wonderfully modest:

> **By Sunday evening, can I walk into a shitty-looking fantasy village and have its inhabitants unexpectedly perform a two-minute musical number about the village without the game falling over?**

If yes, the experiment has worked.

And if the answer is *“sort of, but the innkeeper sang the guard's verse while facing a wall and then everybody danced silently for forty seconds”*, I would argue that the experiment has **especially** worked.

If you want, I'll do the next bit properly: we can turn this into a **copy-paste Nova Weekend Challenge prompt pack**, with a master project prompt followed by staged prompts for your software architect to feed it sequentially, specifically designed so he can basically start Friday night with an empty project and see how far it gets by Sunday.

## User — turn 3

That sounds perfect

## ChatGPT — turn 4

Excellent. I think we should make the pack deliberately **experimental rather than over-specified**. The interesting question isn't whether we can design the whole game on paper; it's how much of this absurd thing Nova can actually bootstrap before your architect has to intervene.

I'd structure the handoff as a Friday-to-Sunday sequence with a hard rule: **don't fix amusing failures unless they prevent progress**.

### Nova Weekend Challenge

**Working title: *The Elder Songs*** — legally, obviously, we will eventually need something that isn't waving quite so enthusiastically at Bethesda.

The master brief I'd give it is roughly:

> Build a playable fantasy RPG prototype in which entering a settlement can trigger an original musical theatre number performed by its inhabitants.
>
> The ordinary game should resemble the basic interaction grammar of an open-world fantasy RPG: free exploration, NPC interaction, dialogue, locations and simple quests. However, musical performance is a fundamental property of the world.
>
> The prototype should favour breadth of experimentation over polish. Placeholder assets, crude animations, simplistic environments and imperfect procedural output are acceptable.
>
> Musical performances may be funny, awkward or technically imperfect. NPCs missing cues, poor choreography, questionable lyrics, strange staging and other non-blocking emergent behaviour should generally be preserved rather than polished away.
>
> Software failures are different. Crashes, broken game state, impossible progression, unrecoverable performances and corrupted saves should be fixed.
>
> **Weekend objective:** create one small fantasy settlement containing approximately 8–12 inhabitants, several buildings, basic NPC interaction and one simple quest. Entering the settlement should trigger an ensemble musical number introducing the place and some of its inhabitants. The quest should provide opportunities for at least two further musical events.
>
> Build systems in a modular way so that settlements, characters, quests and musical numbers can later be generated or expanded procedurally.
>
> Do not attempt to build a complete RPG. At every stage prefer the simplest implementation that produces something playable, surprising and funny.

Then I would **stop**. Let Nova respond, propose its architecture and make some decisions. Your architect should resist the temptation to tell it how to implement everything.

The second prompt becomes:

> **Build the smallest playable non-musical version first.**
>
> Create the settlement, player controller, NPC population, interaction/dialogue system and one very simple quest.
>
> Use existing or generated placeholder assets wherever possible. Visual quality is unimportant.
>
> The settlement and NPCs should nevertheless have enough structured information that another system could reason about them: settlement name, locations, occupations, character names, relationships and quest relevance.
>
> Do not implement music yet.
>
> When this stage is playable, stop and report what exists, what is placeholder, what assumptions you made and what you recommend implementing next.

That's Friday night's checkpoint. **Can we walk around Shitsville and talk to Gerald the inexplicably enormous cheesemaker?**

Then comes the fun prompt.

> **Make the settlement a musical.**
>
> Design and implement a reusable Musical Director system.
>
> A musical number should be triggered by a game event and should have access to current world state. It should determine:
>
> - subject and dramatic purpose;
> - participating NPCs;
> - lead and supporting performers;
> - song structure;
> - lyrics assigned to performers;
> - simple choreography and staging;
> - player involvement where appropriate;
> - start and completion conditions.
>
> Create the first event: when the player enters the settlement for the first time, its inhabitants perform an ensemble number welcoming the player and introducing the settlement.
>
> The lyrics should refer to actual generated facts about the settlement and its inhabitants rather than being entirely pre-written.
>
> Use the most practical available method of producing music, vocals, animation and synchronisation. Prefer an imperfect working implementation over an ambitious non-working one.
>
> **Do not manually author the finished song. The system should construct it.**

That last sentence matters enormously. Otherwise Nova may very helpfully write **“Welcome to Dungleford”** and hard-code the bloody thing, thereby technically completing the assignment while missing the experiment entirely.

Once *anything* vaguely musical happens, Saturday becomes iterative.

Prompt it:

> **Increase theatrical ambition without replacing the existing working system.**
>
> Add formations, entrances, exits, chorus behaviour, camera direction and environmental staging where feasible.
>
> NPCs should move into approximate performance positions rather than simply singing wherever they happen to be.
>
> Allow the Musical Director to use different structures: solo, duet, call-and-response, ensemble and reprise.
>
> Do not require perfect synchronisation. Preserve funny outcomes unless they break progression.

Then introduce the protagonist mechanic:

> **Make the player a participant rather than merely an audience member.**
>
> During suitable numbers, offer the player 2–4 contextually generated lyrical responses.
>
> Selecting a response determines the protagonist's contribution and may alter the remainder of the number, NPC reactions and quest state.
>
> Initially implement this through selection rather than requiring microphone input or actual singing.
>
> The player must retain the ability to make inappropriate, selfish or ridiculous responses rather than always behaving like a heroic musical lead.

That potentially becomes *really* good. It's essentially a dialogue tree in which **the dialogue tree is happening inside a song**.

Then Saturday night: deliberately ruin everything.

> **Chaos test the musical system.**
>
> Create abnormal world states before and during performances. Examples include missing performers, dead or incapacitated performers, performers unable to reach their marks, obstructed routes, combat, the player leaving the performance area, conversations being initiated, objects blocking choreography and multiple events attempting to trigger simultaneously.
>
> A musical number should degrade gracefully rather than crash or permanently block progression.
>
> Develop recovery rules using current world state. Where sensible, reassign lines, omit unavailable performers, alter choreography or continue imperfectly.
>
> **Do not correct merely aesthetic failures.**
>
> After testing, report the five funniest emergent failures you observed and preserve any that do not damage gameplay.

I **really** want that last report.

Sunday is where we discover whether there's a game underneath the joke.

Give it a second musical situation with very different dramatic requirements: perhaps the player has been asked to recover the village's stolen ceremonial turnip. They enter a cave. Bandits sing an ominous villain number. The player can join in. Depending on their lyrical response, this can become combat, negotiation or somehow an audition.

Then:

> Extend the existing quest so that musical interaction can affect gameplay rather than functioning only as presentation.
>
> At least one musical choice must alter quest progression.
>
> At least one NPC should remember something the player sang and reference it subsequently.
>
> Include a reprise later in the quest whose lyrics or tone reflect an earlier player decision.
>
> Do not pre-write the resulting scenes. Extend the generative systems so they produce them from game state.

**That is the point where I'd stop the weekend.**

Because by then you've tested three increasingly interesting propositions:

**Can Nova build a shitty RPG? → Can it make the shitty RPG spontaneously become a musical? → Can the musical itself become an RPG mechanic?**

If only the first works, amusing weekend.

If the second works, you've got a fantastic demo.

If the third works, I think you've accidentally got an actual game concept.

And there is one architectural principle I'd keep hammering into Nova throughout: **generative AI decides what the performance is; deterministic game code remains responsible for making the game work.** You don't want an LLM deciding whether Bernard has successfully walked through a door. You want it saying *“Bernard crosses to stage-left during bar 17 while singing about his failed marriage”*, and conventional game systems doing their best to execute that instruction.

That separation is what could eventually let the ridiculous prototype grow into the polished version you described without throwing everything away.

Also: don't name the village beforehand. **Make Nova invent it.** I have an unreasonable amount riding on discovering what it thinks a fantasy musical village ought to be called.
