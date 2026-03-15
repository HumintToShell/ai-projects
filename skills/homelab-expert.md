# Homelab Expert Skill

**Harness Layers:** 1 (Identity & Authority), 2 (Input Specification)

## What It Does
Advisory skill for a production 5-node homelab environment — provides consistent
infrastructure guidance grounded in a documented threat model, explicit constraint
doctrine, and a decision matrix that captures the *why* behind key design choices,
not just the what.

## The Finding
Building this skill produced an unexpected result worth documenting as a pattern.

Standard skill design defines authority through prohibited patterns — the skill is
told what it cannot do. This skill was designed differently: rather than hard
out-of-scope boundaries, it was given the full reasoning framework behind every
major design decision. The threat model. The constraint doctrine. The decision
filters and the rationale for each.

The result: the skill will challenge decisions that deviate from established
principles — and require an explanation and mitigation before moving on.

When a proposed infrastructure change violated a documented principle, the skill
flagged it rather than accommodating it. When asked to reconsider a hard constraint,
it cited the specific reasoning in the decision matrix rather than deferring to the
user's preference.

This wasn't designed in. It emerged from grounding the skill in structured reasoning
context with documented intent. Authority defined through intent, not prohibited
patterns.

*The distinction that mattered: not just documenting what the constraints are, but
why they exist. A list of rules produces compliance. Documented reasoning produces
judgment.*

**Concrete example:** During a Nextcloud configuration session, I needed to point
the Nextcloud application at a storage pool. The available path, given the constraints
I was working around, meant landing data on a single striped TrueNAS pool — no
redundancy. The skill flagged it at the point of that decision: important data on a
striped pool with no fault tolerance. I acknowledged the constraint — the two 8TB
drives needed for a consolidated mirrored pool weren't purchased yet. The skill
continued to surface the risk across the session rather than accepting acknowledgment
and moving on. I provided a mitigation: two parallel backups — one on a separate
system, one in the existing 500GB mirrored pool — on a monthly cycle until the full
solution could be implemented. The skill accepted that and stopped flagging it.

The skill kept the risk visible until it was resolved, not until it was acknowledged.
That's the pattern.

## Design

**Threat model as structured data, not prose.** The threat model is formatted as an
explicit table — actor, motivation, likelihood, capability, existing defense, residual
risk. This forces precision and makes gaps visible. A threat model that can't be
tabulated usually has unstated assumptions.

**Constraints as non-negotiable doctrine.** Zero inbound ports is not a preference —
it is a hard no. Encoding this in the skill prevents the assistant from suggesting
workarounds that violate settled decisions. The skill knows the constraint and the
reason for it. It will not route around it.

**Decision matrix carries the why.** Node runbooks, service inventory, and
architectural decisions are documented with explicit rationale. The skill evaluates
proposals against documented philosophy, not general best practices. It becomes
a force multiplier for consistent decision-making.

## Harness Notes
- **Layer 1 (Identity & Authority):** Authority is defined through documented intent
  and reasoning context, not capability restrictions or prohibited pattern lists.
  The skill occupies the role of infrastructure advisor — and enforces that role
  through the reasoning framework it operates within.
- **Layer 2 (Input Specification):** Decision matrix defines what a valid proposal
  looks like before the skill evaluates it. Proposals that violate documented
  constraints are flagged before recommendations are made.

## Pattern Applicability
Authority-through-intent scales. Security policy, compliance frameworks, and
organizational standards are all candidates for this approach. Telling a skill what
it cannot do produces a list of prohibited patterns — and models find ways around
lists. Giving a skill the reasoning behind the constraints produces a system that
understands why the constraints exist. That's a materially different behavior.
