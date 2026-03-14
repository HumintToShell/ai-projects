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

| Layer | Contract | Function |
|-------|----------|----------|
| 1 | Identity & Authority | What the agent is *permitted to occupy*, not what it can do |
| 2 | Input Specification | Defines valid input before reasoning begins — HALT on ambiguity, do not infer |
| 3 | Reasoning Constraints | Logic gates built by the SME over time; every conclusion cites a specific input |
| 4 | Adversarial Verification | Separate judge whose only job is to break the worker's output |
| 5 | Human-in-the-Loop Delivery | What the SME receives — confidence scores, audit trails, defined escalation triggers |

The SME provides the load. AI provides the lift. The orchestrator provides the harness.

## Projects

These are presented in the order they were built. Several predate the harness vocabulary — the instincts came first, the framework came from naming what was already happening. That progression is the point.

### Frameworks

**[ScriptForge](./frameworks/scriptforge.md)** — Context-driven AI workflow for generating and optimizing PowerShell scripts to federal enclave standards. A governing document as constraint harness (Layers 1, 3) — before I had the vocabulary for it. The AI never touches production data or systems; environment-specific details are placeholder values the sysadmin fills in before deployment. The closest thing to professional application in this portfolio.

### Workflows

**[LLM Platform Evaluation](./workflows/llm-evaluation.md)** — Four-phase elimination process across six frontier LLM platforms. Identified sycophancy, fixation, and hallucination as evaluation criteria before having formal vocabulary for them. This is adversarial evaluation methodology — the precursor to Layer 4 thinking.

**[Local Context Workflow for Claude Code](./workflows/local-context-pattern.md)** — Filesystem-based AI context management without cloud persistence. Touches all five layers in a thin implementation — model-agnostic architecture designed for environments where cloud tooling isn't an option.

### Skills

**[Homelab Expert Skill](./skills/homelab-expert.md)** — Infrastructure advisory skill encoding a structured threat model, decision filter framework, and hard constraint doctrine (Layers 1, 2). Scope boundary and authority contract in practice — the skill knows what it is not permitted to advise on.

**[Travel Agent Skill](./skills/travel-agent.md)** — Domain expert skill for timeshare vacation planning, ROI tracking, and itinerary building (Layers 2, 3). Input specification and reasoning constraints applied to a real domain workflow with verifiable outputs.

### Agents

**[Session Closer Agent](./agents/closer-agent.md)** — Custom Claude Code agent for structured session documentation and domain-aware note routing (Layer 5). Human-in-the-loop delivery discipline — the agent proposes, the human approves, nothing writes to the vault without explicit authorization.

## In Progress

**IEP Accommodation Generator** — Gemini Gem with Google Workspace integration that generates IEP-accommodated versions of algebra materials (chunked and enlarged formats) as native Google Docs. Built for a real SME — an 8th grade algebra teacher — who needs compliant accommodated materials without manually reformatting every assignment. This is the implementation chasm in miniature: the capability exists, the teacher's time doesn't. Pending deployment while the example template library is built.

## Background

Federal IT Specialist (GS-12), Department of Justice. Windows systems administration across a distributed field office environment — approximately 800 users, one field office plus 15 offsites, including air-gapped enclave management. Active on the agency's AI advisory board. Previously: Army counterintelligence and HUMINT operations, federal law enforcement operations center.

Everything in this portfolio was built personally — homelab systems, personal workflows, and domain-specific tools — unless noted otherwise. The constraints that shape the work are real: air-gapped enclaves, zero inbound ports, and data policies that don't accommodate most AI tooling as-is.

The federal AI adoption problem isn't capability — it's operationalization in constrained environments. That's what this portfolio documents.

---

*All examples sanitized for public sharing. No hostnames, network topology, or implementation-specific details included.*
