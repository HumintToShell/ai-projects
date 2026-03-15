# Session Closer Agent

**Harness Layer:** 5 (Human-in-the-Loop Delivery)

## What It Does
Production agent for structured session documentation — analyzes the conversation,
generates notes split by domain, and routes each to the correct location. The agent
proposes. The human approves. Nothing writes anywhere without explicit authorization.

## The Hard Rule
The Obsidian vault is the committed knowledge repository, not a scratch pad. The
agent knows the difference and cannot cross that line without permission.

Working files live in the Claude Code workspace. Finalized, polished content goes
to the vault — and only when explicitly directed. The agent will never write to
the vault on its own judgment. That boundary is architectural, not advisory.

## Design

**Dynamic domain discovery.** The agent scans the filesystem for active domain
directories identified by the presence of CLAUDE.md — no hardcoded paths. Domain
routing is derived from structure, not maintained as a list.

**Structured output.** Every session note follows a consistent format: summary,
key points, decisions made, documents modified, follow-ups, links. Routed to the
correct domain directory based on session content classification.

**Confirmation before every write.** No auto-save behavior. The agent surfaces
what it intends to write and where before any tool is called. The human decides
what gets committed.

## Architectural Decisions

**Explicit tool formatting.** The generated baseline prompt referenced tools
conversationally. Changed all tool names to backtick-formatted callables (`Glob`,
`Write`, `Read`) to eliminate ambiguity between conceptual references and actual
tool invocations.

**Rejected domain skills dependency.** Evaluated giving the agent access to domain
skills for richer classification context. Rejected it — CLAUDE.md files in each
domain directory already provide sufficient context. Simpler solution that meets
the requirement wins over added complexity.

## Key Finding
The human gate isn't a safety feature added on top of the agent — it's the
architectural requirement the agent was designed around. An agent that could write
anywhere on its own judgment would be a liability in a system where the vault
represents committed knowledge. The constraint defines the design.

## Trade-offs
- Requires explicit invocation — no passive background logging
- Domain classification relies on conversation content analysis, which can be
  ambiguous in multi-topic sessions
- Session notes are only as good as the agent's ability to identify what mattered

## Pattern Applicability
The propose-then-confirm pattern applies to any agent operating in an environment
where writes have consequence. The distinction between working storage and committed
storage — and the hard rule that the agent cannot cross that line without explicit
authorization — is directly applicable to any system where output quality and
authorization matter more than automation convenience.
