# ScriptForge — AI-Assisted PowerShell Development Framework

**Context:** Personal — framework designed around professional deployment constraints

## Problem Statement
Writing consistent, field-ready PowerShell scripts for a distributed federal environment
requires holding a large amount of context: enclave-specific constraints, site naming
conventions, what patterns are explicitly forbidden, and personal style conventions
that make scripts readable and maintainable by junior admins across 56+ offices.
Generic AI-generated scripts don't meet these requirements without significant rework.

## What ScriptForge Is

ScriptForge is a context-driven AI workflow — not a script generator itself, but the
framework that makes Claude Code generate scripts that match how I write them. I bring
a requirement or a rough script; Claude uses the ScriptForge documentation to produce
output built to my specifications.

The name is accurate: raw material goes in, finished product comes out. The
ScriptForge documentation is the die. Claude is the press. The output looks like I
wrote it — because the framework was built from how I write.

## Framework Components

| File | Audience | Purpose |
|------|----------|---------|
| `STANDARDS.md` | Claude | What to include, what to explicitly omit, and why — tuned to enclave reality |
| `PROJECT_CONTEXT.md` | Claude | Environment context: air-gapped enclaves, USB deployment, junior operators, site naming conventions |
| `templates/` | Claude | Base script templates with best practices pre-built |
| `examples/` | Claude | Enhanced real scripts demonstrating standards applied in practice |
| `PROMPTS.md` | Human user | User manual for the framework — how to interact with Claude to get the most out of ScriptForge; intended for anyone who clones the repo and wants to use it |

## Methodology
- I documented my existing script conventions and the constraints of my operational
  environment (STANDARDS.md, PROJECT_CONTEXT.md)
- I built PROMPTS.md as a user manual for anyone cloning the repo — guidance on
  how to interact with Claude for common tasks: generate from requirement, optimize
  existing script, code review against standards, documentation
- I validated the framework against real tasks — a script optimization pass on an
  existing script and a clean generation from a new requirement
- Both produced output that matched my specifications without post-generation rework

## Results
- **Script optimization:** Provided a rough working script; Claude read the ScriptForge
  documentation and returned a standards-compliant version matching my conventions
- **Script generation:** Described a requirement; Claude produced a field-ready script
  built to my specifications, not generic PowerShell best practices
- Output is indistinguishable from scripts I write manually — same structure, same
  conventions, same operational constraints respected

## Validated Use Cases
- Generate new scripts from a plain-language requirement
- Optimize existing rough scripts to ScriptForge standards
- Review scripts against documented standards and identify gaps
- Bring legacy scripts up to current conventions

## Trade-offs
- ScriptForge documentation requires upfront investment to build accurately — the
  framework is only as good as how well it captures the actual environment and style
- Claude never touches production systems or data — I review and deploy all output.
  This is a deliberate constraint, not a limitation.
- Framework must be updated when environment constraints change (new enclave
  configurations, updated site naming conventions, etc.)

## Key Finding
Encoding personal expertise and environmental constraints into a reusable context
framework produces AI output that doesn't require rework. Generic prompts produce
generic scripts. Specific context produces output built to specification.

The framework also solves the federal data sovereignty problem cleanly: AI assists
with code generation in a local development context. No operational data, no
production systems, no network environment ever touches the AI. The output is code
I review and deploy — the same as if I wrote it myself.

## Architectural Decisions

**Documentation over prompts:** Rather than crafting elaborate one-off prompts for
each script, I invested in structured documentation (STANDARDS.md, PROJECT_CONTEXT.md)
that Claude reads at the start of any ScriptForge session. This means any prompt can
be simple — the complexity lives in the framework, not the request.

**Style capture, not just standards:** STANDARDS.md doesn't just document what's
technically correct — it captures how I write. Color-coded output, GridView for
results, progress percentages, user-friendly prompts with examples. The goal is
output I'd be comfortable deploying under my name.

**Explicit forbidden patterns:** Documenting what NOT to include (no module imports,
no enterprise CmdletBinding patterns, no complex logging for quick diagnostics) is as
important as documenting what to include. Enclave environments have real constraints
that generic AI training data doesn't account for.

## Implications
- **Federal/enterprise environments:** The ScriptForge pattern — document your
  environment constraints and personal conventions, use them as AI context — is
  directly applicable to any organization with non-standard operational requirements.
  Air-gapped, classified, or heavily regulated environments all have constraints
  that generic AI output won't respect without explicit documentation.
- **Knowledge transfer:** The ScriptForge documentation is also a living record of
  institutional knowledge — conventions, constraints, and reasoning that would
  otherwise exist only in the developer's head.
- **AI force multiplication:** A sysadmin who can describe what they need in plain
  language and get back deployable code — built to their own standards — is
  significantly more productive than one generating scripts from scratch every time.

## Technical Requirements
- Claude Code CLI
- ScriptForge documentation directory (STANDARDS.md, PROJECT_CONTEXT.md, PROMPTS.md)
- Base templates and examples for reference
- Local PowerShell development environment for review and testing before deployment

## Pattern Applicability
The ScriptForge pattern works for any domain where consistent output to personal or
organizational specifications matters. The framework components — context document,
standards document, prompt library, templates, examples — translate directly to
other scripting languages, configuration management, or documentation workflows.

## Next Steps
- Continue building the examples library as more scripts are generated and validated
- Evaluate whether a CLAUDE.md in the ScriptForge directory would improve session
  startup time
- Document the optimization workflow as a formal use case with before/after examples
