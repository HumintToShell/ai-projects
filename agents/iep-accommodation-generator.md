# IEP Accommodation Generator

**Harness Layers:** 2 (Input Specification), 5 (Human-in-the-Loop Delivery)

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

The SME receives a finished, compliant document in the format she is required
to work in. The Gem never touches anything outside the designated file share.

## Why Gemini
Google Workspace and Google Classroom are the environment the SME is required
to work in. This was not a capability evaluation — it was a constraint. Gemini
is native to that environment. Any other model would have required workarounds
that introduced friction into a workflow the SME needs to be simple.

This is a model-selection-by-constraint decision, not a model-selection-by-
preference decision. The harness architecture is tool-agnostic. The scaffolding
choice followed the deployment environment.

## The Input Layer
The example folder is the input specification for this system. It contains
structured examples of IEP-accommodated algebra materials that teach the Gem
the accommodation patterns for this specific SME and subject area.

A Start Here document governs the folder:

- **File naming convention** — `[Material Type] - [Accommodation] - [Description]`
- **Quality standards** — mathematical accuracy preserved, problem integrity
  maintained, Google Docs native format, Chromebook compatible
- **Self-updating logic** — add better examples, the system improves; remove
  outdated examples, the system adapts

The example library is the harness artifact that requires the most investment.
The Gem is only as good as what the SME puts in the folder. This is intentional —
the SME owns the quality standard, not the model.

## Design

**Layer 2 (Input Specification):** The example folder and Start Here document
define what valid input looks like before the Gem reasons about anything. The
Gem studies the examples, understands the accommodation patterns, then adapts
to new material. The input layer is the governing document — not the prompt alone.

**Layer 5 (Human-in-the-Loop Delivery):** The SME receives a draft Google Doc.
She reviews it before it goes anywhere near a student. The Gem produces the
artifact; the SME owns the output. Compliance decisions stay with the human.

## What Testing Showed
Tested against synthetic algebra materials created to match the expected format.
The Gem correctly applied accommodation patterns from the example folder and
produced native Google Docs output without manual reformatting. The Start Here
document governed folder behavior as designed.

Production validation will surface edge cases the synthetic testing didn't — the
school enterprise account configuration, real SME documentation formats, and
accommodation patterns that didn't appear in the synthetic example set.

## Pattern Applicability
The example-folder-as-input-layer pattern is applicable to any domain where the
quality standard is owned by a subject matter expert, not the developer. The SME
defines quality by curating examples. The model learns from the curation. The
developer's job is to build the folder structure and the governance document —
not to encode every accommodation pattern manually into the prompt.
