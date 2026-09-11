# Prompt engineering musical RPG — shared continuation excerpt

> Orientation only. This is a source snapshot, not adopted project direction.
> See the [source index](README.md) for provenance and limitations.

## ChatGPT — shared response

Ah! **Astra, not Nova.** Yes — and actually it changes my answer in a fairly important and positive way. I was mentally treating “Nova” as an agentic development environment and therefore gave you a broadly sensible agent workflow, but I wasn't grounding it in the thing you actually meant.

GPT-6 Astra is unusually relevant to this experiment. OpenAI specifically highlights **game development, 3D/spatial reasoning and visual judgement** among its improved capabilities, and its game-development examples involve the model actually working with environments rather than merely generating source code. [OpenAI +1](https://openai.com/index/gpt-6-astra/?utm_source=chatgpt.com)

More interestingly, Playco has been testing Astra through Playbot with direct **Unity and Godot** integration: the model can edit scenes, run the game, visually inspect what happened, test it and iterate. They report that Astra produced three themed prototypes from a common grey-box game, with most working on the first attempt and about **50% fewer manual fixes** than their previous-model workflow. [OpenAI](https://openai.com/index/playco-game-prototyping-with-astra/?utm_source=chatgpt.com)

So I'd change our approach in three ways.

**First, I'd be considerably more ambitious about the weekend objective.** I was assuming “get some code and assets assembled and see whether this mad thing vaguely runs.” With Astra, I think the experiment should explicitly exploit its ability to **build → run → look → judge → modify**. The musical-number problem is almost comically well suited to testing that, because choreography is spatial. “Put Bernard here, have the chorus form a semicircle behind him, then have Margaret cross behind the player during the second verse” requires understanding what the resulting scene actually looks like.

**Second, I'd rewrite the prompts so Astra is responsible for iterative playtesting.** Rather than:

> Implement this feature. Stop and tell us what you did.

I'd use:

> Implement this feature. Run the game and test it yourself. Observe the resulting scene and behaviour. Identify functional problems and make further iterations until the acceptance criteria are met. Do not correct harmless visual or theatrical jank merely because it is imperfect. Report what you deliberately chose to leave unfixed.

That's a *much* more interesting instruction for Astra.

**Third — and this is probably the biggest change — I'd give it more creative autonomy.** Astra is reported to be better at resolving underspecified instructions and maintaining context as a task evolves. [OpenAI](https://openai.com/index/gpt-6-astra/?utm_source=chatgpt.com) So I wouldn't over-engineer our prompt pack before the experiment starts.

I'd actually make the opening challenge closer to:

> **You have one weekend to make this idea playable.**
>
> We want a small open-world fantasy RPG in which settlements behave like musical theatre.
>
> The player should be able to explore normally, interact with NPCs and undertake simple quests. However, entering a settlement or reaching dramatically appropriate moments can cause its inhabitants to perform elaborate musical numbers involving singing, dancing, staging and potentially player participation.
>
> The eventual ambition is a genuinely good RPG/musical hybrid, but this prototype should embrace generative chaos. Bad lyrics, dubious choreography, performers missing cues, inappropriate musical choices, awkward staging and other amusing imperfections are desirable emergent behaviour.
>
> Crashes, broken progression and systems that fundamentally don't work are not.
>
> **Your task is to determine the most effective technical route to a playable vertical slice, build it, run it, playtest it, observe the results and iteratively improve it.**
>
> Do not fake generative systems by hard-coding a single demonstration. We are testing whether the underlying idea can work.
>
> Start by proposing the vertical slice and technical architecture you intend to build. Keep it achievable, but surprise us.

And then **see what Astra says**.

I now think giving it my Dungleford architecture upfront would actually spoil part of the experiment. My Musical Director / Performance Controller / structured `MusicalNumber` idea might turn out to be exactly right — but let's see whether **Astra invents something better**.

Then your architect becomes the **producer/director**, rather than the programmer. He spends the weekend saying things like:

> “Good. Now make the player participate in the song.”

> “The dancing is too competent. Don't improve it.”

> “Can these three NPCs perform a reprise based on what happened in the quest?”

> “Kill the lead singer before the number and see what happens.”

> “That was hilarious. Preserve that behaviour.”

That's a much purer test of what has suddenly become possible.

And wonderfully, someone has already demonstrated Astra autonomously playing through *Portal* using screenshots and positional information — not a benchmark, but another indication that this sort of **observe a 3D game → understand what's happening → act → observe again** loop is now genuinely interesting. [Tom's Hardware](https://www.tomshardware.com/tech-industry/artificial-intelligence/openais-gpt-6-astra-model-autonomously-completes-portal-in-24-hours-feat-cost-just-usd571-in-tokens?utm_source=chatgpt.com)

So yes: **the concept stays; the staged weekend structure stays; but I would substantially rewrite the actual prompt pack for Astra and give it less implementation prescription and much more authority to build, observe and iterate.**

In fact, now that I know you meant **Astra specifically**, I'm rather more intrigued by the experiment than I was before. This is a gloriously unreasonable way of finding out what the new model can actually do.

---

If you want, I can:

- Develop a detailed weekend project plan for Astra with iterative playtesting steps
- Draft the initial open-world musical RPG vertical slice proposal Astra might produce
- Outline a rehearsal of Astra iteratively directing and modifying the prototype
