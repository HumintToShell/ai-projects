# IEP Accommodation Generator

**Harness Layers:** All (1–5)

## Status
Designed and tested against synthetic documents in a personal Gemini sandbox.
Production validation pending — the school enterprise Google Workspace is a
different configuration than the development environment, and the example library
is being built from real SME documentation. Deployment target: end of school year,
when the example library can be built out properly with the SME.

## What It Does
A Gemini Gem with Google Workspace integration that generates IEP-accommodated
algebra materials as native Google Docs — built for a real SME with a real
compliance requirement who saves hours reformatting every assignment.

The Gem produces three accommodation types — Chunked (content grouped by topic
or complexity), Enlarged (font and spacing adjustments for visual accessibility),
and Standard (baseline comparison) — as finished Google Docs ready for Google
Classroom and Chromebook use. The SME receives compliant documents in the format
she is required to work in. Mathematical content is never altered.

## Why Gemini
Google Workspace and Google Classroom are the environment the SME is required
to work in. Gemini is native to that environment. Any other model would have
required workarounds that introduced friction into a workflow the SME needs to
be simple. This is a model-selection-by-constraint decision, not a
model-selection-by-preference decision. The harness architecture is tool-agnostic.
The scaffolding choice followed the deployment environment.

## All Five Layers Applied

**Layer 1 (Identity & Authority):** The Gem's identity is explicitly scoped —
IEP accommodation specialist for 8th/9th grade algebra materials. Not a general
document formatter. Not a general education assistant. The role is narrow, the
subject area is specific, and the authority boundary is defined before any task
begins.

**Layer 2 (Input Specification):** Four accepted input methods are defined —
document name, Google Drive link, pasted content, or attachment. Each has a
documented handling path. File association rules map accommodation requests to
template files: "Chunking" → files with "Chunked" in title, "Enlargement" →
files with "Enlarged" in title. Ambiguity handling is specified: search Drive
first, ask one clarifying question if needed, never refuse based on input format.

The reference folder (`[IEP_ACCOMMODATION_TEMPLATES]`) is the authoritative
source. The Start Here document is read at the beginning of every task — it
defines the current template inventory and governs how the folder is used.

**Layer 3 (Reasoning Constraints):** Two hard constraints are non-negotiable
and documented as such:

- *Mathematical integrity* — problem content, numerical values, and correct
  answers are never altered. The accommodation changes how information is
  presented, not what the information is.
- *Output format* — ALL outputs are native Google Docs. Word, PDF, and any
  other format are explicitly prohibited. District compatibility (Google
  Classroom, Chromebook, print-correct) is a documented requirement.

**Layer 4 (Adversarial Verification):** A pre-delivery verification step is
built into the execution workflow. Before any document is delivered, the Gem
confirms: no content accidentally omitted, mathematical accuracy preserved,
formatting matches template patterns, output is native Google Docs format.
Verification is not optional — it is Step 6 of a six-step workflow.

**Layer 5 (Human-in-the-Loop Delivery):** The SME receives a draft Google Doc
with a delivery summary and flagged concerns. She reviews before anything
reaches a student. Compliance decisions stay with the human. The Gem produces
the artifact — the SME owns the output.

## The Baseline/Override Pattern
The prompt establishes a two-layer instruction hierarchy worth documenting as
a design pattern:

*"Your learned patterns provide the BASELINE. My specific instructions provide
the OVERRIDE. Apply both intelligently."*

The example folder defines how accommodations are structured by default. The
SME's session instructions override those defaults for specific materials. The
Gem applies both — it doesn't flatten the session instruction into the template
pattern or ignore the template in favor of the session instruction. This produces
consistent output that remains flexible without requiring the SME to re-specify
the full accommodation standard every session.

## The Six-Step Execution Workflow
The prompt encodes a structured execution sequence — not a list of capabilities,
but a defined reasoning path:

1. **Locate** — find the target document using the input method provided
2. **Identify** — determine material type (worksheet, quiz, or test)
3. **Find Templates** — match material type to templates in the reference folder
4. **Learn** — study template structure, formatting, grouping, visual patterns,
   and mathematical notation handling
5. **Rebuild** — apply template's structural DNA to target while preserving
   all mathematical content and following any session-level overrides
6. **Verify** — pre-delivery accuracy check before any output is delivered

The workflow is the reasoning constraint. Each step gates the next. The Gem
does not skip to generation — it locates, identifies, and learns before it builds.

## The Input Layer
The example folder is the input specification for accommodation quality. A Start
Here document governs the folder:

- **File naming convention** — `[Material Type] - [Accommodation] - [Description]`
- **Quality standards** — mathematical accuracy preserved, problem integrity
  maintained, Google Docs native format, Chromebook compatible
- **Self-updating logic** — add better examples, the system improves; remove
  outdated examples, the system adapts

The SME owns the quality standard by curating the example library. The Gem
learns from what is in the folder. The developer's job is to build the folder
structure and the governing document — not to encode every accommodation pattern
manually into the prompt.

## Pattern Applicability
Several patterns in this design are portable:

**Baseline/override instruction hierarchy** — learned patterns as default,
session instructions as override — applies to any domain where the SME needs
consistent output that remains adaptable without re-specifying the full standard
every session.

**Example-folder-as-input-layer** — the SME defines quality by curating
examples; the model learns from the curation — applies to any domain where
the quality standard is owned by a subject matter expert, not the developer.

**Hard constraint documentation** — explicitly marking non-negotiable constraints
as such ("non-negotiable," "NEVER," "MUST") produces different model behavior
than preference language. Mathematical integrity and output format are not
suggestions in this prompt. The language reflects that.
