# AI Projects & Implementations

Practical AI operationalization built under real federal constraints —
where data sovereignty isn't a preference, it's a requirement.

## Background

Federal IT Specialist with 23+ years of operational experience across
Army counterintelligence and federal law enforcement, now managing Windows
infrastructure and support across a large distributed environment.

Everything in this portfolio was built personally — homelab systems,
personal workflows, and domain-specific tools — unless noted otherwise.
The constraints that shape the work are real: air-gapped enclaves, zero
inbound ports, and data policies that don't accommodate most AI tooling as-is.

The closest thing to professional application here is ScriptForge — a
framework that generates sanitized PowerShell scripts from sanitized
examples. Environment-specific details like OUs and directory paths are
placeholder values the sysadmin fills in before deployment. The AI never
touches production data or systems.

The federal AI adoption problem isn't capability — it's operationalization
in constrained environments. That's what this portfolio documents.

## Projects

### Agents
- [Session Closer Agent](./agents/closer-agent.md) — Custom Claude Code agent for structured session documentation and domain-aware note routing

### Skills
- [Homelab Expert Skill](./skills/homelab-expert.md) — Infrastructure advisory skill encoding a structured threat model, decision filter framework, and hard constraint doctrine; evolved from a subagent implementation to native skill architecture
- [Travel Agent Skill](./skills/travel-agent.md) — Domain expert skill for timeshare vacation planning, ROI tracking, and itinerary building; evolved from a subagent implementation to native skill architecture

### Workflows
- [Local Context Workflow for Claude Code](./workflows/local-context-pattern.md) — Filesystem-based AI context management without cloud persistence
- [LLM Platform Evaluation](./workflows/llm-evaluation.md) — Four-phase elimination process across six frontier LLM platforms; behavioral testing methodology and decision framework for selecting a primary AI assistant

### Frameworks
- [ScriptForge](./frameworks/scriptforge.md) — Context-driven AI workflow for generating and optimizing PowerShell scripts to personal specifications and federal enclave standards; includes user documentation for others who want to clone and use the framework

## In Progress

- **IEP Accommodation Generator** — Gemini Gem with Google Workspace integration that generates IEP-accommodated versions of algebra materials (chunked and enlarged formats) as native Google Docs; pending deployment while example template library is being built

---
*Note: All examples sanitized for public sharing. No hostnames, network topology, or implementation-specific details included.*
