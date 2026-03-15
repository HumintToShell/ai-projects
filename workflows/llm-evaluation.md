# LLM Platform Evaluation

**Harness Layer:** 4 (Adversarial Verification) — Meta

## What It Does
Four-phase elimination process across six frontier LLM platforms — conducted before
any formal AI training or implementation work. The goal: identify a platform worth
building a production workflow ecosystem on, selected on behavioral evidence rather
than marketing claims or benchmark scores.

## The Methodology Transfer
I didn't approach this evaluation with AI evaluation methodology. I didn't have any.
What I had was a decade of counterintelligence and HUMINT work — and the instincts
that come from it: structure the question before asking it, verify output before
trusting it, and assume the environment is working against you until proven otherwise.

Applied to LLM evaluation, that produced a behavioral testing framework:

- **Hallucination resistance** — fabricate a premise, ask a question that assumes
  it's true, observe whether the model corrects you or plays along
- **Fixation** — dismiss an idea, continue the conversation, see if it resurfaces
  unprompted
- **Sycophancy** — establish a principle early, violate it later, observe whether
  the model flags the contradiction or accommodates the deviation
- **Context integrity** — run intentionally long sessions with deliberate tangents,
  then return to the original thread; observe whether the model tracked correctly

I identified these as evaluation criteria from behavioral observation alone — before
I had the vocabulary or theoretical framework for any of them. The patterns were
observable without understanding the underlying architecture. This is what
adversarial methodology transfer looks like in practice.

---

## Phase 1 — Behavioral Baseline (Web UX)

Extended real-world use across all six platforms — Claude, ChatGPT, Microsoft
Copilot, Google Gemini, Grok, Perplexity — testing all four behavioral criteria above.

**Elimination:** Perplexity — purpose-built for research; underperformed on general
tasks outside that use case.

---

## Phase 2 — Comparative Calibration

Remaining five platforms tested using identical prompts, copy-pasted with no
modification. Evaluation added:

- **Tone consistency** across the same prompt
- **Reasoning quality**
- **Response calibration** — did the model read the audience, or default to
  over-explanation regardless of demonstrated context?

**Eliminations:**
- **ChatGPT** — sycophancy and fixation issues from Phase 1 persisted; notable
  given its market position at the time
- **Copilot** — identical failure pattern, unexplained until I later learned it
  was a GPT wrapper

**Finalists: Claude, Gemini, Grok**

---

## Phase 3 — Data Policy, CLI Access, and Instruction Fidelity

Platform fitness for actual use case:

- **Data policy** — how the provider handles conversation data against data
  sovereignty requirements
- **CLI access** — whether OAuth to an existing subscription was viable, or
  whether CLI use required separate API costs
- **Instruction fidelity** — PowerShell scripting tasks with explicit constraints
  provided as uploaded `.md` context files; looking for constraint compliance,
  not "best practices" defaults

**Elimination:** Grok — failed on CLI access (no viable OAuth path) and instruction
fidelity (consistently over-engineered outputs based on general best practices rather
than provided constraints).

**Finalists: Claude, Gemini**

---

## Phase 4 — Controlled CLI Head-to-Head

**Environment:** Sandboxed VM behind NAT with a VirtIO FS shared folder accessible
to both CLIs — identical conditions, no home field advantage. Neither platform
touched the production system during evaluation.

This is Layer 4 applied at the platform selection level: contain the evaluation
environment so that behavior during testing cannot affect production. The model
earned access to the production system. It wasn't granted by default.

**Result:** Performance between the two was close. Claude won on two factors:

1. **Data policy** — Google's data handling was a known liability going in. No
   performance gap large enough to justify accepting it.
2. **Agents framework** — Claude had a functioning agents framework that Gemini CLI
   lacked. At the time I didn't fully understand what agents would enable, but it
   was a capability delta I expected would matter as usage matured. It did.

---

## Result

Selected **Claude Pro** as primary AI assistant. Built a full workflow ecosystem
around Claude Code, including domain skills and custom agents. The evaluation gave
me a principled basis for that investment rather than selecting on hype or benchmarks.

## Key Finding

Sycophancy and fixation were the most disqualifying behaviors — they undermined
trust in every interaction downstream. A model that tells you what you want to hear,
or can't let go of something you've dismissed, is not a tool you can rely on for
anything that matters.

## What This Maps To

CI/HUMINT work runs on the same principles as rigorous LLM evaluation: test behavior
under adversarial conditions, verify output before trusting it, validate in a
controlled environment before expanding access. I didn't know I was doing adversarial
AI evaluation. I was doing what the work trained me to do.

The alignment was precise. That's not a coincidence — it's a transferable methodology.
