# ScriptForge — AI-Assisted PowerShell Development Framework

**Harness Layers:** 1 (Identity & Authority), 3 (Reasoning Constraints)

## What It Does
A constraint framework for AI-assisted PowerShell development — built to personal
enclave standards, portable to any LLM with repo access. The governing documents
define what gets generated and what doesn't.

Scripts are generated or enhanced in a personal environment using sanitized context.
Output matches how I write — structure, conventions, style. The sanitized script is
then ported to the production enclave and adapted there: OUs filled in, file paths
corrected, enclave-specific values added. The AI produces the artifact. The human
carries it across the boundary and completes it. Published on GitHub as a byproduct
of the architecture, not the goal.

## The Architecture
ScriptForge is the clearest example in this portfolio of the harness/scaffolding
distinction in practice.

The repo is the harness — STANDARDS.md, PROJECT_CONTEXT.md, templates, examples.
Deterministic. Doesn't change when the model changes. Written as policy, not as
model-specific syntax. The LLM is the scaffolding — temporary, probabilistic,
swappable. Any model with access to the repo can run ScriptForge. The output is
consistent because the framework is consistent, not because of which model is
executing it.

This was built as production infrastructure for a user of one. The portability
was intentional: it doesn't matter what system I'm on or what LLM I'm using —
the framework travels with the repo.

## Framework Components

| File | Audience | Purpose |
|------|----------|---------|
| `STANDARDS.md` | Claude | What to include, what to explicitly omit, and why — tuned to enclave reality |
| `PROJECT_CONTEXT.md` | Claude | Environment context: air-gapped enclaves, USB deployment, junior operators, site naming conventions |
| `templates/` | Claude | Base script templates built to my specific conventions and structure |
| `examples/` | Claude | Enhanced real scripts demonstrating standards applied in practice |
| `PROMPTS.md` | Human user | User manual for the framework — how to interact with Claude to get the most out of ScriptForge; intended for anyone who clones the repo and wants to use it |

## Methodology
- Documented existing script conventions and the constraints of the operational
  environment (STANDARDS.md, PROJECT_CONTEXT.md)
- Built PROMPTS.md as a user manual for anyone cloning the repo — guidance on
  how to interact with Claude for common tasks: generate from requirement, optimize
  existing script, code review against standards, documentation
- Validated the framework against real tasks — a script optimization pass on an
  existing script and a clean generation from a new requirement
- Both produced output that matched specifications without post-generation rework

## Results
- **Script optimization:** Provided a rough working script; Claude read the ScriptForge
  documentation and returned a standards-compliant version matching conventions
- **Script generation:** Described a requirement; Claude produced a field-ready script
  built to specification, not generic PowerShell best practices
- Output closely matches scripts written manually — same structure, same conventions,
  same operational constraints respected. Close enough that the difference requires
  deliberate scrutiny to find.

## Validated Use Cases
- Generate new scripts from a plain-language requirement
- Optimize existing rough scripts to ScriptForge standards
- Review scripts against documented standards and identify gaps
- Bring legacy scripts up to current conventions

## Harness Notes
- **Layer 1 (Identity & Authority):** The governing documents define what the AI
  is permitted to generate — and what it is not. Forbidden patterns are documented
  explicitly. The AI operates within the scope the framework defines.
- **Layer 3 (Reasoning Constraints):** STANDARDS.md encodes environment-specific
  constraints, style conventions, and the reasoning behind each. Generic AI training
  data doesn't account for air-gapped enclaves, USB-only deployment, or junior
  operator readability requirements. The framework does.

## Key Finding
Encoding personal expertise and environmental constraints into a reusable context
framework produces AI output that doesn't require rework. Generic prompts produce
generic scripts. Specific context produces output built to specification.

The framework also solves the data sovereignty problem cleanly: AI assists with
code generation in a local development context. No operational data, no production
systems, no network environment ever touches the AI. The output is code reviewed
and deployed by the human — the same as if written manually.

## Architectural Decisions

**Documentation over prompts:** Rather than crafting elaborate one-off prompts for
each script, the complexity lives in the framework documentation, not the request.
Any prompt can be simple. The framework handles the rest.

**Style capture, not just standards:** STANDARDS.md doesn't just document what's
technically correct — it captures how I write. Color-coded output, GridView for
results, progress percentages, user-friendly prompts with examples. The goal is
output deployable under my name.

**Explicit forbidden patterns:** Documenting what NOT to include is as important
as documenting what to include. Enclave environments have real constraints that
generic AI training data doesn't account for.

## Pattern Applicability
The ScriptForge pattern works for any coding workflow where consistent output to
personal or organizational specifications matters. The repo is open — clone it,
replace the context documents with your own environment and conventions, and the
framework runs on any LLM you point at it.

The same principle extends beyond code. A knowledge-as-code environment — where
documentation, policy, or institutional knowledge is structured and version-controlled
— can use this exact framework with modifications. Replace STANDARDS.md with your
documentation conventions. Replace PROJECT_CONTEXT.md with your domain context.
The governing documents still define what gets generated and what doesn't. The
scaffolding is still swappable. The harness travels with the repo.
