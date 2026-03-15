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

## Projects

These are presented in the order they were built. Several predate the harness vocabulary — the instincts came first, the framework came from naming what was already happening. That progression is the point.

### Frameworks

**[ScriptForge](./frameworks/scriptforge.md)** — A constraint framework for AI-assisted PowerShell development — built to my own enclave standards, portable to any LLM with repo access. The governing documents define what gets generated and what doesn't; the AI never touches production systems or data. Published on GitHub as a byproduct of the architecture, not the goal. Layers 1, 3.

### Workflows

**[LLM Platform Evaluation](./workflows/llm-evaluation.md)** — Four-phase elimination process across six frontier LLM platforms — conducted before any formal AI training or implementation work. I wasn't applying AI evaluation methodology; I was applying adversarial methodology from a decade of CI/HUMINT work. It happened to align precisely with how LLM capability should actually be evaluated. Identified sycophancy, fixation, and hallucination as criteria from behavioral observation alone, before having the vocabulary for them. Meta / Layer 4.

**[Local Context Workflow for Claude Code](./workflows/local-context-pattern.md)** — Filesystem-based AI context management without cloud persistence. Designed for environments where cloud tooling isn't an option — all five harness layers implemented through local files and folder structure alone. Layer 4 applied at the deployment level: the model running this workflow lived in a sandboxed VM for several weeks of adversarial testing before being trusted on the production system. Simple by necessity, portable by design. All Layers.

### Skills

**[Homelab Expert Skill](./skills/homelab-expert.md)** — Advisory skill for a production 5-node homelab environment — built around a defined threat model and a decision matrix that documents the *why* behind key design choices, not just the what. Rather than hard out-of-scope boundaries, the skill is given enough context to reason at the edges of its domain. A discovered side effect: grounding an LLM in structured reasoning context with documented intent largely eliminates sycophancy within that domain — the skill will challenge decisions that deviate from established principles and require an explanation and mitigation before moving on. Authority defined through intent, not prohibited patterns. Layers 1, 2.

**[Travel Agent Skill](./skills/travel-agent.md)** — Production skill for managing a timeshare ownership — real booking decisions, real ROI calculations verifiable against market rates. Operates in two distinct modes: destination brainstorming against available inventory and points constraints, or itinerary building once a trip is booked. Each mode has its own input specification and reasoning constraints. Outputs are defensible, not just plausible. The trips get booked from this. Layers 2, 3.

### Agents

**[Session Closer Agent](./agents/closer-agent.md)** — Production agent for structured session documentation — analyzes the conversation, generates notes split by domain, and routes each to the correct location. The agent proposes, the human approves, nothing writes anywhere without explicit authorization. Built around a hard rule: the Obsidian vault is the committed knowledge repository, not a scratch pad — the agent knows the difference and cannot cross that line without permission. Layer 5.

## In Progress

**IEP Accommodation Generator** — Gemini Gem with Google Workspace integration that generates IEP-accommodated algebra materials as native Google Docs — built for a real SME with a real compliance requirement who saves hours reformatting every assignment. Google Workspace and Google Classroom are the environment the SME is required to work in — Gemini was the right tool for that constraint, deployed in a sandboxed VM with controlled file access only. The SME gets a finished, compliant document. The AI never touches anything outside the file share. Pending deployment while the example template library is built. Layers 2, 5.

## Background

Federal IT Specialist (GS-12), Department of Justice. Windows systems administration across a distributed field office environment — approximately 800 users, one field office plus 15 offsites, including air-gapped enclave management. Active on the agency's AI advisory board. Previously: Army counterintelligence and HUMINT operations, federal law enforcement operations center.

Everything in this portfolio was built personally — homelab systems, personal workflows, and domain-specific tools — unless noted otherwise. The constraints that shape the work are real: air-gapped enclaves, zero inbound ports, and data policies that don't accommodate most AI tooling as-is.

The federal AI adoption problem isn't capability — it's operationalization in constrained environments. That's what this portfolio documents.

---

*All examples sanitized for public sharing. No hostnames, network topology, or implementation-specific details included.*
