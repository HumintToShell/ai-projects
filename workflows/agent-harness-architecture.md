# Agent Harness Architecture (Independently Designed)

**Harness Layers:** All (1–5)

## The Problem Came First

This framework wasn't designed to look like any open-source tool. It was designed to
solve a specific problem: managing a growing collection of AI domain skills, persistent
context, and remote agent sessions across a 5-node homelab — without cloud
dependencies, without inbound ports, and without losing context between sessions.

Built in two phases between November and December 2025, driven entirely by operational
need. The instinct came first. The vocabulary came later.

The local context workflow (documented [here](./local-context-pattern.md)) was the
seed. Phase 1 formalized it into a full harness. Phase 2 extended it to remote access.

## Timeline

| When | What | Why |
|------|------|-----|
| **Nov 1, 2025** | CLI-first AI strategy documented; AI sandbox baseline established | Needed portable context that survived sessions and model switches — no cloud, no lock-in |
| **Nov 21, 2025** | Full Base Contexts architecture finalized: operator context, threat model, constraints, nodes-and-roles, remote access strategy | All six context documents written in a single working session — the framework architecture complete |
| **Nov 23, 2025** | CLAUDE.md local context pattern implemented | Framework moved from design documents into daily operational use |
| **Nov 24, 2025** | Clawdbot (later OpenClaw) publishes its initial alpha on GitHub | One day after CLAUDE.md; three days after the full Base Contexts architecture |
| **Dec 2025** | Twingate + Termux + SSH remote access (zero inbound ports) | Needed mobile access to persistent workspace sessions from the field |
| **Late Jan 2026** | OpenClaw goes viral | Framework had been in daily operational use for two months by this point |
| **Feb 2026** | Anthropic ships Claude Code Remote Control | Migrated to it as a cleaner implementation of the existing remote pattern |

Every component was built when the operational need emerged — not in response to a
trend, not as a monolithic project. The trend arrived after the fact.

## Architecture

### Phase 1 — Local Context Layer (November 2025)

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

When Anthropic shipped Claude Code Remote Control in February 2026, the migration was
to a cleaner implementation of a pattern already running in daily operational use for
two months.

## What This Demonstrates

- Architecture-level AI systems thinking, not just tool use
- Ability to reason about what an agent framework actually requires — memory, context
  portability, skill modularity, secure remote access — and build it from first
  principles before those requirements had names in the open-source community
- Phased, operationally driven design: each component built when the need emerged,
  not as a monolithic project
- LLM-agnostic design discipline: the framework works because the architecture is
  sound, not because it's tied to one platform
- Security posture applied at the design layer, not bolted on after the fact

## External Validation

When OpenClaw went viral in early 2026, the architecture it popularized matched what
had already been built here independently — model-agnostic context layer, persistent
memory, modular skills, and zero-inbound-port remote access. The Base Contexts
architecture was finalized November 21, 2025; Clawdbot (OpenClaw's initial alpha)
appeared November 24. Two independent paths arrived at the same architecture because
the architecture is correct.

Security posture is stronger by design: this framework requires explicit operator
approval for irreversible actions. OpenClaw defaults to open access and has been
exploited via prompt injection attacks (data exfiltration, code deletion). The approval
model isn't a limitation — it's correct threat modeling applied from the start.

## Resume Bullet

> Built a personal AI agent framework from scratch (Nov–Dec 2025) to solve operational
> problems — model-agnostic context hierarchy, persistent cross-session memory, modular
> domain skills, and secure zero-inbound-port remote access. When open-source tools
> popularizing the same architecture went viral two months later, independent
> convergence validated the design. Security posture was stronger by design: explicit
> operator approval gates, zero inbound ports, sandboxed adversarial testing before
> production deployment.

## Evidence

Timeline claims are supported by filesystem metadata (modify timestamps) from the
original VM environment where development occurred. Key dates: `initial_ai_context.md`
(Nov 1, 2025), Base Contexts architecture files (Nov 21, 2025), `CLAUDE.md` local
context pattern (Nov 23, 2025). Clawdbot (later OpenClaw) published its initial alpha
on GitHub November 24, 2025. Evidence file: `timeline_evidence.txt` (generated from
`stat` output, April 8, 2026).
