# Travel Agent Skill for Claude Code

## Problem Statement
Managing Club Wyndham timeshare vacation planning across multiple booking networks
(Wyndham, WorldMark, Margaritaville, RCI exchanges) required consistent domain context
across sessions: ROI formulas, points economics, trip history, family preferences, and
destination research approach. Rebuilding that context manually each session was
inefficient and error-prone.

## Methodology
- Built initial solution as a domain expert subagent — autonomous agent loaded with
  travel context, planning logic, and ROI tracking methodology
- Validated subagent approach across real trip planning sessions (itinerary building,
  ROI calculation, destination brainstorming)
- Evaluated Anthropic's native skill system upon release and assessed fit against
  existing subagent implementation
- Refactored from subagent to skill, restructuring prompt accordingly
- Maintained dual-mode operation: itinerary planning (destination locked) and
  destination brainstorming (open exploration)

## Results
- Deployed skill provides persistent domain context across all travel planning sessions
- Dual-mode detection: agent reads opening message to determine whether Chris has
  destination/dates locked or is exploring options, and adapts workflow accordingly
- ROI tracking formula embedded: compares points cash equivalent to comparable
  market rental (VRBO/Airbnb) for post-trip analysis
- Trip history (2022-2026) and lessons learned maintained in REFERENCE.md,
  loaded on skill invocation
- Decision filters enforce travel philosophy: geographic clustering over rigid
  schedules, local food over national chains, ROI-justified premiums

## Trade-offs
- Skill context is read-only during session — trip history updates require
  manual edits to REFERENCE.md after each trip
- No live booking integration — availability and reservation mechanics handled
  separately by user
- Family composition treated as session variables (always asked, never assumed),
  which adds a setup step each session but prevents stale assumptions

## Key Finding
Subagents are designed for autonomous task execution with tool use and multi-step
reasoning. Skills are designed for domain expertise injection — loading context,
terminology, and decision frameworks into the assistant's operating mode. The
travel planning use case fit the skill pattern cleanly: no autonomous actions needed,
just consistent context and structured reasoning applied to user-directed tasks.

Using the native skill system over a forced subagent implementation eliminated
unnecessary complexity and aligned the tool choice with its intended design.

## Architectural Decision

**Subagent → Skill refactor:** The original subagent implementation worked, but
subagents carry overhead suited for autonomous, tool-using workflows. Travel planning
is fundamentally interactive — Chris drives decisions, the agent provides analysis and
structure. When the skills system became available, refactoring was the right call:
simpler invocation, lighter footprint, better alignment with how the feature is
designed to work.

This reflects a broader principle: prefer native platform capabilities over custom
implementations that approximate the same behavior. The platform will optimize its
own primitives; fighting the grain adds maintenance burden for no functional gain.

## Implications
- **Federal/enterprise environments:** Domain skill pattern is directly applicable to
  any recurring expert consultation use case — policy interpretation, compliance
  checking, standards reference — where consistent context matters more than
  autonomous action
- **Skill vs. agent decision framework:** If the use case requires autonomous tool
  execution and multi-step reasoning without user involvement, use an agent. If it
  requires domain expertise applied to user-directed tasks, use a skill. Travel
  planning is the latter.
- **ROI documentation as discipline:** Embedding ROI tracking methodology into the
  skill enforces consistent analysis across trips, building a multi-year dataset
  rather than one-off calculations

## Technical Requirements
- Claude Code CLI with skills support
- SKILL.md defining invocation triggers and core identity
- REFERENCE.md for persistent domain data (trip history, ROI formulas, lessons learned)
- Obsidian vault for finalized trip documents (user-directed writes only)

## Pattern Applicability
The domain expert skill pattern — core identity and decision logic in SKILL.md,
persistent reference data in REFERENCE.md — is reusable for any domain with stable
context that needs to persist across sessions. Homelab infrastructure, policy
compliance, field-specific analysis, and similar domains follow the same structure.

## Next Steps
- Update REFERENCE.md post-trip with New Orleans 2026 ROI data
- Evaluate whether annual points tracking should be broken into a separate tracked
  document or maintained inline
- Consider a third mode for post-trip ROI documentation workflow
