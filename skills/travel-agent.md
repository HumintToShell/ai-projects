# Travel Agent Skill

**Harness Layers:** 2 (Input Specification), 3 (Reasoning Constraints)

## What It Does
Production skill for managing a timeshare ownership — real booking decisions, real
ROI calculations verifiable against market rates. The trips get booked from this.

## Design

**Dual-mode operation.** The skill operates in two distinct modes with different
input specifications and reasoning constraints:

- **Destination brainstorming** — open exploration against available inventory,
  points balance, and travel calendar. Input spec: points available, travel window,
  family composition, preferences. Output: ranked options with points cost and
  estimated ROI against market rates.
- **Itinerary building** — destination and dates locked, building a day-by-day
  plan. Input spec: confirmed reservation details, family composition, interests,
  logistics constraints. Output: structured itinerary with activity clustering,
  local food prioritization, and contingency options.

Mode is detected from the user's opening message — not selected from a menu. The
skill reads whether destination and dates are locked and adapts accordingly.

**ROI tracking embedded.** Every trip is evaluated against a comparable market
rental — the skill searches for an actual comp: vacation rental (VRBO/Airbnb)
matching property type, size, and location for the same dates. Not a hotel room,
not an approximation. The formula is embedded in the skill, the comp search uses
defined criteria, and the output is a verifiable number. This builds a multi-year
dataset rather than one-off calculations. Outputs are defensible, not just plausible.

**Decision filters encode travel philosophy.** Geographic clustering over rigid
schedules. Local food over national chains. ROI-justified premiums. These aren't
preferences stated at the start of each session — they're embedded in the skill's
reasoning framework and applied before recommendations are made.

## Harness Notes
- **Layer 2 (Input Specification):** Each mode has a defined input spec. The skill
  determines which spec applies before reasoning begins. Family composition is always
  asked, never assumed — session variable, not persistent assumption.
- **Layer 3 (Reasoning Constraints):** ROI formula, decision filters, and trip
  history are encoded as reasoning constraints. The skill evaluates options against
  documented criteria, not general travel advice.

## On the Subagent→Skill Refactor
This skill started as a domain expert subagent. When Anthropic released the native
skill system, I refactored. Subagents carry overhead suited for autonomous,
tool-using workflows — travel planning is interactive and user-directed. The refactor
was straightforward because the harness didn't change. The governing documents,
decision filters, and ROI methodology stayed identical. Only the scaffolding changed.
That's the point.

## Key Finding
Dual-mode operation with separate input specifications produces materially different
output quality than a single general-purpose travel assistant. The skill knows what
it needs before it starts reasoning — and the mode determines what "done" looks like.

## Trade-offs
- Skill context is read-only during session — trip history updates require manual
  edits to REFERENCE.md after each trip
- No live booking integration — availability and reservation mechanics handled by
  the user
- Family composition treated as a session variable — adds a setup step but prevents
  stale assumptions

## Pattern Applicability
The dual-mode input specification pattern applies to any domain where the same
subject area requires fundamentally different reasoning depending on where the user
is in the decision process. The mode determines the input spec. The input spec
determines the reasoning constraints. The reasoning constraints determine what a
defensible output looks like.
