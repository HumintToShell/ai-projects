# Local Context Workflow for Claude Code

**Harness Layers:** All (1–5)

## What It Does
Filesystem-based AI context management without cloud persistence — all five harness
layers implemented through local files and folder structure alone. Designed for
environments where cloud tooling isn't an option, or where data sovereignty is a
non-negotiable constraint.

This is the workflow currently running in this portfolio's homelab environment.

## Layer 4 Came First
Before this workflow was trusted on the production system, the model running it had
to earn that access.

Phase 4 of the LLM platform evaluation ran Claude and Gemini head-to-head in a
sandboxed VM behind NAT — identical conditions, no access to production systems or
data. That evaluation was the adversarial verification step. Claude passed. The VM
came down. The workflow moved to the production system.

Layer 4 isn't a feature of this workflow — it's a precondition for it. The
deployment discipline happened before the deployment.

## How It Works
- Local directory structure mirrors the context management a cloud Project provides
- CLAUDE.md carries identity, operating philosophy, constraints, and domain context
- All five harness layers implemented through file structure and documented policy:
  - **Layer 1 (Identity & Authority):** Defined in CLAUDE.md — role, scope, what
    the model is permitted to occupy
  - **Layer 2 (Input Specification):** Context files define valid inputs and
    operating parameters before reasoning begins
  - **Layer 3 (Reasoning Constraints):** Decision frameworks, constraint doctrine,
    and domain logic encoded as reference files loaded on invocation
  - **Layer 4 (Adversarial Verification):** Completed in the sandboxed VM prior to
    production deployment — not embedded in the workflow itself
  - **Layer 5 (Human-in-the-Loop Delivery):** Nothing writes to committed storage
    without explicit human approval; the human remains the decision point

## Key Finding
Projects and persistent cloud memory are primarily UI conveniences. Core AI
capability operates effectively with filesystem-based context management. The
harness doesn't require cloud infrastructure — it requires discipline in how
local files are structured and maintained.

## Trade-offs
- Requires directory navigation before starting a session
- Device-dependent without a sync solution (mitigated via Nextcloud)
- Manual version control responsibility
- No automatic cross-device synchronization

## Pattern Applicability
Tested with Claude Code, but deployment-agnostic. The same pattern works with
self-hosted models in air-gapped or classification-constrained environments — the
model is stateless, all context lives on the workstation, and the harness travels
with the files. Simple by necessity, portable by design.
