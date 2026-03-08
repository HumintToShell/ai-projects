# LLM Platform Evaluation — Selecting a Primary AI Assistant

**Context:** Personal

## Problem Statement

Before committing to a paid AI subscription and building workflows around a platform, I needed a systematic way to evaluate the available frontier LLMs against each other. Marketing claims and benchmark scores don't reflect how a model actually behaves over sustained, real-world use. I ran a four-phase elimination process with six platforms to find one worth building on.

## Methodology

Testing was conducted entirely on empirical observation — no formal AI training, no background in model architecture or training scaffolding. The evaluation was behavioral: does the model do what I need it to do, the way I need it done, under conditions I actually work in.

**Platforms evaluated:** Claude, ChatGPT, Microsoft Copilot, Google Gemini, Grok, Perplexity

---

### Phase 1 — Behavioral Baseline (Web UX)

Extended real-world use across all six platforms, testing:

- **Context retention** — intentionally long conversations with deliberate tangents, then returning to the original topic to see if the model tracked correctly
- **Fixation** — whether the model re-surfaced dismissed ideas or abandoned threads later in context without prompting
- **Hallucination resistance** — I fabricated historical "facts" and asked questions that assumed a false premise was true, to probe whether the model would correct me or play along
- **Sycophancy** — how readily the model would push back on something I said that was wrong or contradicted a principle established earlier in the conversation, versus how often it simply agreed to avoid friction

**Phase 1 eliminations:**
- **Perplexity** — purpose-built for research; underperformed on general tasks outside that use case

---

### Phase 2 — Comparative Calibration

The remaining five platforms were tested using identical prompts, copy-pasted with no modification. Evaluation focused on:

- **Tone consistency** across the same prompt
- **Reasoning quality**
- **Response calibration** — did the model read the audience? Did it over-explain things I demonstrably already knew, or did it give surface-level responses even on topics where depth was warranted?

**Phase 2 eliminations:**
- **ChatGPT** — poor Phase 1 baseline continued into Phase 2; sycophancy and fixation issues persisted
- **Copilot** — same result (I later learned Copilot was a GPT wrapper, which explained the identical failure pattern)

**Finalists: Claude, Gemini, Grok**

---

### Phase 3 — Data Policy, CLI Access, and Instruction Fidelity

Platform fitness for my actual use case:

- **Data policy** — how the provider handles conversation data and whether it aligns with my data sovereignty preferences
- **CLI access** — specifically whether OAuth to an existing subscription was viable, or whether CLI use required separate API costs on top of a paid plan
- **Instruction fidelity** — I assigned PowerShell scripting tasks with specific constraints provided as uploaded `.md` context files. I was looking for compliance with explicit instructions, not "best practices" defaults

**Phase 3 elimination:**
- **Grok** — failed on both CLI access (no viable OAuth path; third-party workarounds offered only temporary free access) and instruction fidelity (consistently produced over-engineered scripts based on general best practices rather than the constraints I provided)

**Finalists: Claude, Gemini**

---

### Phase 4 — Controlled CLI Head-to-Head

Even though Google's data policy was a liability, I advanced Gemini to Phase 4: if it significantly outperformed Claude in a controlled environment, it might be worth the tradeoff.

**Environment:** Sandboxed VM behind NAT with a VirtIO FS shared folder accessible to both CLIs — identical conditions, no home field advantage.

**Result:** Performance between the two was close. Claude won on two factors. First, data policy — Google's data handling was a known liability going in, and since Claude performed equivalently, there was no performance gap large enough to justify accepting it. Second, Claude had a functioning agents framework that Gemini CLI lacked. At the time I didn't fully understand what agents would enable, but it was a capability Claude had and Gemini didn't, and I expected it would matter as my usage matured.

## Results

- Selected **Claude Pro** as primary AI assistant
- Built a full workflow ecosystem around Claude Code, including custom agents and domain skills
- The evaluation gave me a principled basis for the investment rather than selecting on hype or benchmarks

## Key Finding

Sycophancy and fixation were the most disqualifying behaviors — they undermined trust in every interaction downstream. A model that tells you what you want to hear, or can't let go of something you've dismissed, is not a tool you can rely on for anything that matters.

## Notable Findings

- **ChatGPT's sycophancy was surprising** — at the time it was the clear market leader, with Claude still largely positioned as the developer and coding tool. I expected stronger behavioral performance; the degree to which it avoided friction was notable
- **Copilot's identical failure pattern** was unexplained until I later learned it was a GPT wrapper
- **All of this testing preceded formal AI training** — I identified sycophancy, fixation, and hallucination as evaluation criteria before I had the vocabulary or theoretical framework for them. The behavioral patterns were observable without understanding the underlying architecture

## Implications

Benchmark scores measure capability ceilings. Behavioral evaluations under real working conditions reveal which models are actually trustworthy as long-term tools. For sustained, high-stakes use — especially in environments where data policy matters — running your own elimination process is worth the time.
