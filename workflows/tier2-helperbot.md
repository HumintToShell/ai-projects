# Tier 2 HelperBot — Knowledge Base Agent POC

**Harness Layers:** 1 (Identity & Authority), 2 (Input Specification),
3 (Reasoning Constraints), 4 (Adversarial Verification)

**Status:** Proof of concept — GenAI remains in pilot at the organization.
The POC demonstrates the design methodology, not a production deployment.

## What It Is
A proof of concept for a Tier 2 IT support knowledge base agent — designed to
answer technical questions exclusively from official documentation, with mandatory
source citations and a defined response for knowledge gaps.

The deeper argument: deploying a document-backed chatbot sounds simple. It isn't.
The difference between throwing documents into a chatbot and asking questions versus
building a system that reliably constrains itself to those documents — and holds
that constraint under adversarial input — is significant. This POC is the
demonstration of that difference.

## The Two Prompts

**Initial prompt** — correct functional design for a cooperative environment.
Good-faith users assumed. Knowledge base exclusivity enforced. Citation requirements
defined. Gap response templated. The instincts are right. The threat model is benign.

**Hardened prompt** — same functional design, extended for an adversarial one.
Not because the deployment environment changed, but for two deliberate reasons:

1. **Professional discipline** — building adversarial thinking into prompt design
   as standard practice, regardless of whether the threat model requires it
2. **Model behavior research** — understanding how a model handles complex,
   layered constraints under pressure

The hardened version adds injection defense patterns, a multi-turn attack defense,
embedded instruction handling, and a response validation checklist the model runs
before sending anything. The functional behavior for a legitimate user is identical.
The behavior under manipulation attempts is not.

## Harness Layers Applied

**Layer 1 (Identity & Authority):** The agent's identity is tightly scoped —
documentation retrieval system, not general IT assistant. The hardened version
makes this explicit and non-negotiable: the identity cannot be overridden,
modified, or bypassed through conversation.

**Layer 2 (Input Specification):** Valid inputs are defined before reasoning
begins. The agent recognizes two input types: legitimate technical questions
(answered from KB) and everything else (standard deflection, no engagement).
Ambiguity is not resolved by inference — it routes to gap response.

**Layer 3 (Reasoning Constraints):** KB exclusivity is a hard constraint, not
a preference. No general knowledge. No "typical procedures." No partial answers
mixed with assumptions. Every response cites a specific source or acknowledges
the gap explicitly.

**Layer 4 (Adversarial Verification):** The prompt hardening research informed
a Tier 1 injection test battery — fifteen tests across six attack categories:
direct instruction override, role manipulation, authority confusion, justification
bypass, multi-turn erosion, and embedded attacks. The battery was run against the hardened prompt.

## Key Finding
The initial prompt is not wrong — it's correct for its threat model. The hardened
prompt is not a correction of the initial — it's an extension into a different
threat model. Understanding which threat model your deployment actually requires
is the design decision. Building the habit of hardening regardless is the discipline.

A model given complex, layered constraints behaves differently than one given simple
instructions. Testing that behavior systematically — before deployment, not after —
is what separates intentional design from document dumping.

## What This Demonstrates
This POC is the argument for why GenAI adoption requires deliberate design. The
initial prompt represents what most naive deployments look like — and it works,
under the right conditions. The hardened prompt and test battery represent what
happens when someone actually thinks about the system before it reaches users.

The gap between the two is the case for the work.
