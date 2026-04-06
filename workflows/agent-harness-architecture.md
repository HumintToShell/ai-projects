# Agent Harness Architecture (Independently Designed)

**Harness Layers:** All (1–5)

## The Problem Came First

This framework wasn't designed to look like any open-source tool. It was designed to
solve a specific problem: managing a growing collection of AI domain skills, persistent
context, and remote agent sessions across a 5-node homelab — without cloud
dependencies, without inbound ports, and without losing context between sessions.

Built in two phases between October and December 2025, driven entirely by operational
need. When open-source AI agent harnesses went viral in early 2026, the architectural
pattern they popularized was the same one already running in production here. The
convergence wasn't inspiration — it was independent confirmation that the
architecture is correct.

The local context workflow (documented [here](./local-context-pattern.md)) was the
seed. Phase 1 formalized it into a full harness. Phase 2 extended it to remote access.
The instinct came first. The vocabulary came later.

## Timeline

| When | What | Why |
|------|------|-----|
| **Oct 2025** | CLAUDE.md context hierarchy + persistent memory + domain skill modules | Needed portable context that survived sessions and model switches — no cloud, no lock-in |
| **Dec 2025** | Twingate + Termux + SSH remote access (zero inbound ports) | Needed mobile access to persistent workspace sessions from the field |
| **Jan 2026** | OpenClaw goes viral — same architecture, 100k+ GitHub stars | Independent convergence; this framework had been running in production for 2–3 months |
| **Feb 2026** | Anthropic ships Claude Code Remote Control | Migrated to it as a cleaner implementation of the existing remote pattern |

Every component was built when the operational need emerged — not in response to a
trend, not as a monolithic project. The trend arrived after the fact.

## Architecture

### Phase 1 — Local Context Layer (October 2025)

**Context layer:** A structured CLAUDE.md hierarchy — project-level and
workspace-level markdown files encoding operational context, domain knowledge,
threat models, and workflow preferences. Any capable LLM CLI with filesystem access
can ingest these files and resume with full operational context. No proprietary format,
no platform lock-in. Model-agnostic by design, not as an afterthought.

This is the same pattern documented in the [Local Context Workflow](./local-context-pattern.md)
entry — that entry covers the filesystem-level implementation; this entry covers the
architectural pattern it instantiates and its evolution into a full agent harness
with remote access.

**Persistent memory:** A cross-session memory system that retains user profile,
workflow preferences, and project state across conversations. Survives session
boundaries. Survives model switches.

**Domain skill modules:** Reusable context packages invoked by name — Homelab Expert,
Travel Agent, Faith Assistant, OSINT Team, Session Closer. Each encodes domain
knowledge and operational constraints rather than scripted workflows, preserving
operator control over orchestration. Skills are Layer 1 and 2 implementations:
authority and input specification defined through intent.

### Phase 2 — Remote Access (December 2025)

**Remote access:** Secure mobile access to persistent workspace sessions with zero
inbound ports. Implemented via Twingate (zero-trust network access), Termux (Android
terminal), and SSH — full mobile CLI access to the T7810 without exposing any inbound
ports.

This is the same capability open-source agent harnesses later shipped as a product
feature. It also predates Anthropic's own solution: when Anthropic shipped Claude Code
Remote Control in February 2026, the migration was to a cleaner implementation of a
pattern already running in production for two months.

## Independent Convergence

When OpenClaw went viral in early 2026, the architecture it popularized matched what
had already been built here — across both core capabilities:

1. **Context/memory/skills layer:** OpenClaw's central value proposition is a
   model-agnostic context and skill platform. The CLAUDE.md hierarchy, persistent
   memory system, and domain skill modules built in October 2025 serve the identical
   architectural role — portable context that any LLM CLI can ingest.

2. **Remote agent access:** OpenClaw connects users to their agents remotely. The
   Twingate + Termux + SSH stack deployed in December 2025 solves the same problem
   with a stronger security posture (zero inbound ports), and predates both OpenClaw's
   viral moment and Anthropic's native Remote Control feature.

Two independent paths arrived at the same architecture because the architecture is
correct. That's the validation — not the star count.

Security posture is better by design: this framework requires explicit operator
approval for irreversible actions. OpenClaw defaults to open access and has been
exploited via prompt injection attacks (data exfiltration, code deletion). The approval
model isn't a limitation — it's correct threat modeling applied from the start.

## What This Demonstrates

- Architecture-level AI systems thinking, not just tool use
- Ability to reason about what an agent framework actually requires — memory, context
  portability, skill modularity, secure remote access — and build it from first
  principles before those requirements had names in the open-source community
- Phased, operationally driven design: each component built when the need emerged,
  not as a monolithic project
- LLM-agnostic design discipline: the framework works because the architecture is
  sound, not because it's tied to one platform
- Independent architectural discovery: every component was built from operational
  need months before the pattern had a name — the framework predates the trend it
  aligns with
- Security posture applied at the design layer, not bolted on after the fact

## Resume Bullet

> Built a personal AI agent framework from scratch (Oct–Dec 2025) to solve operational
> problems — model-agnostic context hierarchy, persistent cross-session memory, modular
> domain skills, and secure zero-inbound-port remote access — months before the
> open-source community converged on the same architecture in tools like OpenClaw
> (100k+ GitHub stars, early 2026). Independent design validated by convergence,
> not inspired by it.
