# Homelab Expert Skill for Claude Code

## Problem Statement
Homelab infrastructure decisions require consistent domain context across sessions:
threat model, hard constraints, node inventory, remote access architecture, and a
decision philosophy rooted in operational security principles. Rebuilding that context
manually each session produced inconsistent guidance and forced re-litigating settled
design decisions.

## Methodology
- I built the initial solution as a domain expert subagent — an autonomous agent loaded
  with infrastructure context, threat model, decision filters, and node documentation
- I validated the subagent approach across real infrastructure planning sessions
  (hardware acquisition decisions, remote access design, resilience planning)
- I evaluated Anthropic's native skill system upon release and assessed fit against my
  existing subagent implementation
- I refactored from subagent to skill, restructuring the prompt to match the skill format
- I maintained the full decision filter framework and threat model in REFERENCE.md,
  loaded on skill invocation

## Results
- Deployed skill provides persistent infrastructure context across all homelab sessions
- Decision filters are embedded in the skill and applied before any recommendation is
  made — family friction, inbound exposure, budget priority, resilience, single points
  of failure
- Threat model encoded as a structured assessment: actor profiles, likelihood,
  capability, existing defenses, and residual risk — not a list of fears, but a
  reasoned acceptance table
- REFERENCE.md carries the full lab inventory (node roles, services, listening ports,
  known issues), remote access architecture, and a tiered acquisition roadmap
- Skill prevents re-litigating settled decisions — constraints are documented as
  non-negotiable red lines, not suggestions

## Trade-offs
- REFERENCE.md is static between sessions — node state and inventory require manual
  updates after significant infrastructure changes
- Skill depth creates a large context load on invocation — acceptable tradeoff for
  the consistency it provides
- Decision filters are opinionated and domain-specific; they encode my threat model
  and constraints, not a general-purpose homelab framework

## Key Finding
The homelab skill encodes a reasoning framework, not just reference facts. The decision
filters, threat model, and constraint tables mean the skill doesn't just answer
questions — it evaluates proposals against a documented philosophy before responding.
This is a materially different use of the skill system than simple domain knowledge
injection.

Same subagent-to-skill conclusion as my travel agent implementation: the use case
is fundamentally interactive and user-directed. No autonomous tool execution needed.
The skill system is the right primitive.

## Architectural Decisions

**Subagent → Skill refactor:** Same reasoning as my travel agent refactor — subagents
carry overhead suited for autonomous, tool-using workflows. Infrastructure advisory
is interactive. The user (me) evaluates options; the skill provides the framework for
consistent evaluation. When the skill system became available, the refactor was
straightforward.

**Threat model as structured data, not prose:** I formatted the threat model as an
explicit table — actor, motivation, likelihood, capability, existing defense, residual
risk — rather than descriptive paragraphs. This forces precision and makes gaps
visible. A threat model that can't be tabulated usually has unstated assumptions.

**Hard constraints as non-negotiable red lines:** Constraints are documented
explicitly as doctrine, not preferences. Zero inbound ports is not "I prefer to avoid
inbound ports" — it is a hard no with no exceptions. Encoding this in the skill
prevents the assistant from suggesting workarounds that violate settled decisions.

**REFERENCE.md carries live state:** Node runbooks, current service inventory, and
known issues are maintained in REFERENCE.md as a snapshot. This gives the skill
current operational context, not just architecture intent.

## Implications
- **Federal/enterprise environments:** The decision filter and structured threat model
  approach is directly applicable to enterprise security architecture. Encoding
  constraints as explicit doctrine (not preferences) is standard in policy-driven
  environments — this is the same pattern applied to a personal lab.
- **AI-assisted infrastructure advisory:** Embedding a threat model and decision
  framework into a skill means the AI evaluates proposals against documented
  security posture rather than offering generic best practices. The skill becomes
  a force multiplier for consistent decision-making, not just a search engine.
- **Skill vs. agent decision framework:** Consistent with my travel agent finding —
  domain expertise applied to user-directed decisions belongs in a skill. Autonomous
  remediation or monitoring would belong in an agent.

## Technical Requirements
- Claude Code CLI with skills support
- SKILL.md defining core identity, operating philosophy, and decision filters
- REFERENCE.md for persistent domain data (node inventory, threat model,
  constraints, remote access architecture, acquisition roadmap)

## Pattern Applicability
The decision filter pattern — encoding constraints as explicit doctrine within a skill
rather than relying on the user to re-state them — is applicable to any domain with
non-negotiable operating principles. Security policy, compliance frameworks, and
organizational standards are all candidates for this approach.

## Next Steps
- Update REFERENCE.md node runbooks after each significant infrastructure change
- Evaluate whether the acquisition roadmap should be versioned separately as it evolves
- Consider whether a companion agent (autonomous monitoring or alerting) would
  complement the advisory skill
