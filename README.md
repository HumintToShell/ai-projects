# AI Orchestration Portfolio

Most AI work starts with the model. This portfolio starts with the constraint.

Twenty-three years of operational experience — Army counterintelligence and HUMINT, federal operations centers, and federal IT — taught me one consistent lesson: capability without control is a liability. A decade in counterintelligence and HUMINT built something specific: the instinct to structure a question before asking it, verify output before trusting it, and assume the environment is working against you until proven otherwise. In a federal operations center, you work from structured playbooks — if X, then Y — while maintaining enough situational awareness to know where that information flows and what it triggers downstream. You verify before it goes to the field, because the consequences of wrong information aren't abstract. Federal IT means managing constrained environments where the rules aren't uniform — different enclaves, different policies, different lines you don't cross. Understanding the constraint map is as important as understanding the technology.

These aren't separate careers. They're a through-line — and they converge on a single problem: building AI systems that work within real constraints, fit the domain they're deployed in, and produce outputs reliable enough to act on.

That's not a capability problem. It's a design problem.

## The Harness Architecture

Everything in this portfolio is organized around a framework I call the Harness Architecture. The core distinction:

- **Scaffolding** (agents, LLMs): temporary, probabilistic, powerful — swapped as models improve
- **Harness** (the product): permanent infrastructure — deterministic constraints, security boundaries, logic gates, audit trails

The harness is model-agnostic. It contains zero model-specific syntax. Written as policy, translated by a thin adapter layer. The harness doesn't change. The adapter does.

The architecture operates across five layers:

| Layer | Governs | Function |
|-------|---------|----------|
| 1 | Identity & Authority | What the agent is *permitted to occupy*, not what it can do |
| 2 | Input Specification | Defines valid input before reasoning begins — HALT on ambiguity, do not infer |
| 3 | Reasoning Constraints | Logic gates built by the SME over time; every conclusion cites a specific input |
| 4 | Adversarial Verification | Harden prompts, test behavior against failure modes, and contain deployment so errors don't reach production |
| 5 | Human-in-the-Loop Delivery | What the SME receives — audit trails, defined escalation triggers, and explicit human decision points |

The SME provides the load. AI provides the lift. The orchestrator provides the harness.

A note on terminology: In current technical usage, 'harness' typically refers to the software layer that manages an AI agent while it's running — tool dispatch, memory, safety checks. This portfolio uses the term at a higher level. Here, the harness is the governing framework that defines what the system is permitted to do, what it must produce, and what constraints it operates within — before any technical implementation begins. Think of it this way: the technical community's harness manages how an agent runs. This portfolio's harness defines what the agent is allowed to be. The difference is the same as the difference between a rulebook and the values that produced it.

## Projects

These are presented in the order they were built. Several predate the harness vocabulary — the instincts came first, the framework came from naming what was already happening. That progression is the point.

### Frameworks

**[ScriptForge](./frameworks/scriptforge.md)** — A constraint framework for AI-assisted PowerShell development — built to my own enclave standards, portable to any LLM with repo access. The governing documents define what gets generated and what doesn't; the AI never touches production systems or data. Published on GitHub as a byproduct of the architecture, not the goal. Layers 1, 3.

### Workflows

**[LLM Platform Evaluation](./workflows/llm-evaluation.md)** — Four-phase elimination process across six frontier LLM platforms — conducted before any formal AI training or implementation work. I wasn't applying AI evaluation methodology; I was applying adversarial methodology from a decade of CI/HUMINT work. It happened to align precisely with how LLM capability should actually be evaluated. Identified sycophancy, fixation, and hallucination as criteria from behavioral observation alone, before having the vocabulary for them. Meta / Layer 4.

**[Local Context Workflow for Claude Code](./workflows/local-context-pattern.md)** — Filesystem-based AI context management without cloud persistence. Designed for environments where cloud tooling isn't an option — all five harness layers implemented through local files and folder structure alone. Layer 4 applied at the deployment level: the model running this workflow lived in a sandboxed VM for several weeks of adversarial testing before being trusted on the production system. Simple by necessity, portable by design. All Layers.

**[Agent Harness Architecture](./workflows/agent-harness-architecture.md)** — The local context workflow extended into a full agent framework — model-agnostic context layer, persistent cross-session memory, modular domain skills, and zero-inbound-port remote access — built from operational need between October and December 2025. When open-source agent harnesses went viral in early 2026, the architecture they popularized was already running in production here. Independent design validated by convergence, not inspired by it. All Layers.

**[Tier 2 HelperBot](./workflows/tier2-helperbot.md)** — Proof of concept for a documentation-constrained IT support agent — built to demonstrate that deploying a knowledge base chatbot requires intentional design, not document dumping. Two prompt versions document the progression from functional design to hardened design, with an injection test battery developed alongside the hardening work. The gap between the two versions is the argument. Layers 1, 2, 3, 4. *POC — GenAI in pilot at the organization.*

### Skills

**[Homelab Expert Skill](./skills/homelab-expert.md)** — Advisory skill for a production 5-node homelab environment — built around a defined threat model and a decision matrix that documents the *why* behind key design choices, not just the what. Rather than hard out-of-scope boundaries, the skill is given enough context to reason at the edges of its domain. A discovered side effect: grounding an LLM in structured reasoning context with documented intent largely eliminates sycophancy within that domain — the skill will challenge decisions that deviate from established principles and require an explanation and mitigation before moving on. Authority defined through intent, not prohibited patterns. Layers 1, 2.

**[Travel Agent Skill](./skills/travel-agent.md)** — Production skill for managing a timeshare ownership — real booking decisions, real ROI calculations verifiable against market rates. Operates in two distinct modes: destination brainstorming against available inventory and points constraints, or itinerary building once a trip is booked. Each mode has its own input specification and reasoning constraints. Outputs are defensible, not just plausible. The trips get booked from this. Layers 2, 3.

### Agents

**[Session Closer Agent](./agents/closer-agent.md)** — Production agent for structured session documentation — analyzes the conversation, generates notes split by domain, and routes each to the correct location. The agent proposes, the human approves, nothing writes anywhere without explicit authorization. Built around a hard rule: the Obsidian vault is the committed knowledge repository, not a scratch pad — the agent knows the difference and cannot cross that line without permission. Layer 5.

## In Progress

**[IEP Accommodation Generator](./agents/iep-accommodation-generator.md)** — Gemini Gem with Google Workspace integration that generates IEP-accommodated algebra materials as native Google Docs — built for a real SME with a real compliance requirement who saves hours reformatting every assignment. Google Workspace and Google Classroom are the environment the SME is required to work in — Gemini was the correct tool selection, not a workaround. The prompt and governing documents were designed and tested in a Gemini sandbox; production will live in the school's enterprise system. The example folder is the input layer — structured examples teach the Gem the accommodation patterns; better examples produce better output. Pending deployment while the example library is built. Layers 2, 5.

## Patterns

**Requirement-first design.** Every system in this portfolio started with a defined operational requirement — not available tooling. Pain point identified, tasks decomposed, constraints documented, architecture modeled, then built. The harness gets designed before the scaffolding gets selected — because the requirement determines the tools, never the reverse. This instinct predates AI entirely — it's the same process applied to source collection planning, operations center playbooks, and enclave management for two decades. AI is the newest domain it's been applied to, not its origin. → *All Projects*

**Authority through intent, not prohibited patterns.** Giving a system the reasoning behind its constraints produces judgment. Giving it a list of rules produces compliance. These behave differently under pressure. → *Homelab Expert*

**Generate-then-refine.** AI output is a starting point, not a deliverable. The architectural decisions made after generation — what to keep, what to reject, what to restructure — are where the design actually happens. → *Session Closer, HelperBot*

**Harness before scaffolding.** Build the governing documents first. The LLM is the last thing added, not the first. When the model changes, the harness doesn't. → *ScriptForge, Local Context Workflow*

**Validate before expanding access.** No system earns production access by default. Behavioral testing in a controlled environment precedes deployment. → *LLM Evaluation, Local Context Workflow*

**Input specification determines output quality.** Define what a valid input looks like before reasoning begins. Mode detection, constraint doctrine, and gap response handling are all input-layer decisions. → *Travel Agent, HelperBot*

**Build from need, name later.** Every system in this portfolio started as a solution to a specific operational problem — the architectural vocabulary came from reflecting on what had already been built. The agent harness framework predates the open-source community's convergence on the same pattern by months. The local context workflow predates the formal harness vocabulary entirely. When the problem is real, the right architecture tends to emerge. → *Local Context Workflow, Agent Harness Architecture*

The federal AI adoption problem isn't capability — it's operationalization in constrained environments. That's what this portfolio documents.

---

*All examples sanitized for public sharing. No hostnames, network topology, or implementation-specific details included.*
