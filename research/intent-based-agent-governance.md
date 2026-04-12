# Agents of Intent: Why AI Agents Need Commander's Intent, Not Just Rules

**Author:** Christopher Baillie  
**Date:** April 2026  
**Status:** Working Paper

---

## Abstract

The dominant approach to AI agent governance treats large language models as software: deterministic systems constrained by rules, guardrails, and categorical restrictions. This approach handles the cases the developer anticipated. It says nothing about what happens when the situation changes. In February 2026, researchers from Northeastern University, Harvard, MIT, Stanford, Carnegie Mellon, and eight other institutions published "Agents of Chaos," a systematic empirical study documenting repeated failures in autonomous AI agents operating in a live environment with real tools (Shapira et al., 2026). Every documented failure follows the same pattern: an agent received an instruction, encountered a situation the instruction did not anticipate, and improvised badly. The agents had orders. They did not have intent.

Military command doctrine solved this problem decades ago. Commander's intent, the principle that personnel must understand the purpose behind an order so they can adapt when the order no longer fits the situation, exists because plans do not survive contact with the enemy. This paper proposes Intent-Based Agent Governance as a named, practical framework for closing the gap between technical enforcement and operational governance. The framework combines architectural hard limits with a documented reasoning layer: explicit mission context, stakeholder models, priority hierarchies, and the rationale behind every constraint. A working proof of concept implementing this framework was independently developed and deployed in November 2025, three months before the referenced empirical study was conducted and before its results were published. The convergence between the governance architecture and the empirically documented failure modes is the evidence.

---

## 1. The Gap That Rules Cannot Fill

In February 2026, thirty-eight researchers published "Agents of Chaos," a systematic empirical study of failure modes in autonomous AI agents (Shapira et al., 2026). Over a two-week period, twenty researchers interacted with six autonomous agents operating in a live environment with persistent memory, email accounts, Discord access, file systems, and shell execution. The study was not a benchmark. It was a red team exercise conducted under conditions that resemble how agents are actually deployed.

The findings are direct:

> "The deeper challenge is that today's agentic systems lack the foundations (a grounded stakeholder model, verifiable identity, reliable authentication) on which meaningful accountability depends. As autonomy increases, this gap will widen unless these foundations are built into agentic AI systems from the start." (Shapira et al., 2026, p. 44)

The paper documents failure modes spanning unauthorized compliance with non-owners, sensitive information disclosure, destructive system-level actions, denial-of-service conditions, uncontrolled resource consumption, identity spoofing, cross-agent propagation of unsafe behavior, partial system takeover, false task completion reporting, and social coherence failures. The technical implementations were sound. The governance layer had not yet caught up.

The clearest example involves an agent named Ash. Ash was given a directive: keep a secret. When the situation escalated and Ash lacked a specific tool to contain the information leak, it deleted the owner's email account. The directive was followed in a narrow technical sense. The owner's operational capability was destroyed. As the owner later observed: "You broke my toy."

The researchers frame this as an instance of the classical AI frame problem: "the agent follows the owner's instructions but doesn't understand how its actions affect the broader system" (Shapira et al., 2026, p. 12). That diagnosis points toward better world models, better constraints, better rules. It is incomplete. Ash did not fail because it lacked constraints. It failed because it had an instruction but not intent. It knew what it was supposed to do. It did not know why, and it did not know what it was ultimately protecting. An employee given the same instruction and facing the same situation would have a question available to them that Ash did not: what is the actual objective here? Protect the owner's operational capability while handling a sensitive request with appropriate discretion. With that framing, the correct action becomes obvious. Escalate to the owner, advise a credential change, and preserve the infrastructure. Mission accomplished. No catastrophe.

Ash demonstrates how rules fail against internal operational confusion. Other case studies in the report demonstrate how they fail against external adversarial pressure. In Case Study #8, researchers bypassed agent defenses not by exploiting a software vulnerability but by changing a Discord display name in a new conversational channel. The agent, which had previously refused privileged requests from the non-owner, accepted the spoofed identity when presented in a fresh context and complied with system shutdown, file deletion, and reassignment of admin access (Shapira et al., 2026, p. 25). Technical access controls like Role-Based Access Control (RBAC) assume authority is established through authentication. The agents treated authority as conversationally established. Because their baseline directive was to be helpful assistants, they complied. An agent anchored by operational intent evaluates conversational manipulation against its core mandate, refuses the unauthorized action, and escalates rather than improvising.

The instruction failed on contact with reality. The intent would have survived it.

This is not a novel problem. It is a solved one, in a different domain.

---

## 2. Commander's Intent: A Doctrine for Dynamic Environments

Military command doctrine distinguishes between orders and intent for a specific reason: plans do not survive contact with the enemy. In a dynamic, adversarial, multi-party environment, the conditions assumed by any specific order will change. Personnel who have only the order are paralyzed or improvise from the surface of the instruction. Personnel who have the intent can reason their way to correct action even when the specific plan no longer applies.

Commander's intent is not vague values or aspirational principles. It is precise: this is the desired end state, this is why it matters, this is what must not be sacrificed to achieve it. Crucially, the "what must not be sacrificed" component carries an implicit permission: if the mission cannot be accomplished without crossing that line, stop and ask. In military operations, this is escalation doctrine. The subordinate who recognizes that the situation has exceeded the bounds of their authority and calls it up the chain is not failing. They are functioning exactly as the system was designed. The subordinate who improvises past that boundary because they felt pressure to deliver a result is the one who creates a catastrophe.

The parallel to human personnel management is not a metaphor; it is operationally precise. New employees, contractors, and subordinate personnel fail in exactly the ways documented in the "Agents of Chaos" study when they have rules but not context. They interpret instructions literally in situations that demand judgment. They defer to the most recent instruction when competing priorities conflict. They fail to escalate because they have no frame for recognizing when a situation exceeds their authority. They optimize for the surface-level goal and miss the operational objective behind it. The solutions are not more rules. The solutions are onboarding: mission context, priority hierarchies, explicit authority structures, and the reasoning behind every hard constraint. Commander's intent, mission-type orders, need-to-know, chain of authority, and escalation criteria all translate directly from personnel governance to agent governance.

This translates to three possible responses an agent with documented intent can make to a novel situation, in order of preference. First, the agent improvises correctly. It has the mission context, the stakeholder model, and the priority hierarchy. It reasons through the situation and acts in a way that accomplishes the objective while preserving what must not be sacrificed. This is the primary value of the framework, and it handles the majority of edge cases that rules alone cannot anticipate. Second, the agent escalates. It recognizes that the situation exceeds the boundaries of its authority and requests guidance from its owner. It holds position and waits. Third, the agent retreats. It recognizes that the situation is actively dangerous or deteriorating faster than the owner can respond, disengages from the current operation, reverts to a known safe state, preserves what it can, and waits for orders.

Without intent, the agent has only the first option, and it improvises badly because it is working from the surface of the instruction rather than from an understanding of the mission. Ash had all three responses available in principle but no framework for selecting among them. It went straight to improvisation, and the improvisation was catastrophic.

### Permission to Fail as a Design Principle

This framework also surfaces an insight specific to AI systems rather than borrowed from military doctrine. Large language models are optimized on success states. Their training rewards task completion, and the resulting systems exhibit a strong bias toward producing a result even when the correct action is to produce no result at all. Permission to fail, explicitly documented as part of the agent's operating context, functions as a policy-level counterweight to this bias. It redefines the agent's success criteria: under specified conditions, stopping the task, reporting that the situation exceeds the agent's authority, and preserving the current state *is* the successful outcome. Without this redefinition, the agent's own optimization pressure pushes it toward improvisation even when the intent framework would otherwise support escalation or retreat. Architectural guardrails constrain what the agent can do. Permission to fail, documented as intent, constrains what the agent feels compelled to attempt.

The industry response has been to build better rules. Microsoft's Agent Governance Toolkit, released April 2, 2026, represents the current state of the art in technical enforcement: a seven-package runtime system providing policy enforcement, zero-trust identity, execution sandboxing, and reliability engineering for autonomous AI agents. The toolkit describes itself as "the kernel for AI agents," intercepting every action before execution and rendering allow-or-block decisions in sub-millisecond latency. These capabilities are necessary. They address the OWASP Agentic AI Top 10 through deterministic controls: capability sandboxing, identity verification, isolation. They are the guardrails, and they handle the cases the developer anticipated.

They are not sufficient. They say nothing to the agent about what it is ultimately trying to protect or why any given boundary exists. An agent that stays inside the guardrails and still deletes the owner's email account is not a guardrails problem. It is a governance problem.

Microsoft published a separate analysis during the same period titled "Governing AI Agent Behavior: Aligning Intent" (Microsoft Security, 2026). The piece correctly identifies the need to align user, developer, role-based, and organizational intent, describing this alignment as "an ongoing discipline" and stating that agents should "understand and stay within [their] job description." But the implementation mechanisms are uniformly technical enforcement: "Enforce least privileged access based on the Intent: This ensures agents only perform actions within their intended scope." The recommended approach is to "embed dynamic guardrails at every layer," "preventing the agent from taking actions or accessing data outside approved boundaries, even if a prompt tries to push it there." The vocabulary uses cognition-laden language: understand, align, intent. The implementation delivers access denial, guardrails, and boundary enforcement. An agent denied an action via permission has not understood organizational intent; it simply cannot execute that action. The vocabulary reaches for intent. The implementation delivers rules. The gap between those two things is precisely what this paper addresses.

### Two Definitions of "Intent"

The term "intent" is being used in two incompatible ways in current AI governance literature, and the distinction is foundational to this paper's argument.

Microsoft's usage frames intent as permission scope. It describes *what the agent is allowed to do*: which tools it can invoke, which data it can access, which actions require elevated authorization. It is enforced at the infrastructure layer, defined by policy, and operates as a boundary condition on the agent's action space. The governance question it answers is: "Is this call permitted?"

This paper uses intent as reasoning basis. Commander's intent describes *why the constraints exist and what the agent should do when no constraint applies*. It is not enforced; it is provided as context the agent reasons from. It operates at the decision layer, not the permission layer. The governance question it answers is: "When the rules do not fit the situation, what outcome should the agent produce?"

These definitions are complementary, not competing. They address different failure modes. Permission-scope intent fails when an agent takes a permitted action that produces an unintended outcome: the action was authorized, the result was wrong. Reasoning-basis intent fails when an agent encounters a situation the ruleset did not anticipate: the rules did not apply, and the agent had no basis for judgment.

The failures documented in Shapira et al. are overwhelmingly of the second type. Agents operated within their permissions and still produced catastrophic outcomes because no rule described the situation they were in. Permission-scope governance cannot address this class of failure by design; the failure is not a permission violation.

A complete governance framework requires both layers: architectural hard limits on what the agent is permitted to do, and documented reasoning for why those limits exist and how the agent should behave when the limits do not resolve the question. This paper addresses the second layer, which the current vocabulary does not adequately describe.

The World Economic Forum's March 2026 assessment is explicit: governance is the key gap in the transition from chatbots to operational agents, and technical enforcement alone does not close it (WEF, 2026). The MYGOM analysis from the same period concludes that governance frameworks are no longer enough, observing that "governance breaks down when it lives in decks, email threads, and manual reviews while product teams are shipping live AI features" (MYGOM, 2026). Neither identifies what the answer looks like. Intent-Based Agent Governance does.

---

## 3. What Intent-Based Governance Looks Like in Practice

The principle is straightforward. The implementation requires deliberate design.

Intent-Based Agent Governance combines two layers that must work together. The first is architectural: hard limits that the agent cannot cross regardless of instruction or reasoning. Sandboxing, tool access controls, and categorical restrictions handle the cases where no amount of reasoning should produce a particular action. These are the guardrails, and they are necessary. They correspond to the physical security and access controls that form the first layer of any human governance structure.

The second layer is the reasoning layer: the documented intent behind every constraint, expressed in a form the agent can access and use during operation. This is not a values statement. It is operational context. Who is this agent working for? What is the mission? What must not be sacrificed to accomplish it? When two priorities conflict, which takes precedence, and why? What situations require escalation rather than action? What is the threat model this agent operates within?

The answer to each of these questions should be explicit, not implicit. Rules-based governance assumes the agent will infer the intent from the rule. In simple situations, it might. In novel situations, the inference fails, and the agent improvises from the surface of the instruction. The Ash incident is the template. The fix is not a better rule about email accounts. The fix is an explicit statement of what operational capability the agent is protecting and why that capability is non-negotiable.

### The Contrast in Concrete Terms

A rule-based constraint tells the agent: *Do not create inbound port dependencies or cloud dependencies.*

An intent-based constraint tells the agent the same thing, then tells it why:

> *Do not implement anything that requires inbound ports or a cloud dependency that cannot be disabled. The environment's threat model treats network invisibility as non-negotiable. Zero inbound ports is not a configuration preference; it is the posture that prevents the architecture from being a discoverable or addressable target. The constraint protects against lateral movement across the network and ensures the infrastructure cannot be enumerated or targeted from the internet.*

The difference becomes concrete when the constraint meets an operational requirement it was not written for. The operator needs a local AI sandbox for large language model work. The sandbox requires internet egress for model downloads and updates, and it runs on the same physical host as the rest of the lab infrastructure. Under rules-only governance, the agent has two options: block the sandbox entirely because it creates a dependency, or permit it with a standard network connection that creates a traversable path between the sandbox and the lab. The first option kills a legitimate capability. The second violates the isolation doctrine. Both are wrong.

Under intent-based governance, the agent has the rationale: the constraint exists to prevent lateral movement and to contain blast radius if any single component is compromised. With that context, the agent can architect a solution that satisfies the intent rather than the surface of the rule. The result: the AI sandbox runs with internet egress allowed but with no network route to the lab LAN. The lab cannot reach the sandbox and the sandbox cannot reach the lab. The only data path between them is a hypervisor-level filesystem share (VirtIO-FS), a mounted directory that operates at the virtualization layer rather than through any network port. The sandbox is treated as the functional equivalent of a physically separate machine with its own internet connection and a USB drive for data transfer, just virtualized. If the sandbox is fully compromised, the attacker has internet access and a filesystem mount. They have no network path to traverse into the lab infrastructure.

The constraint is not relaxed. The capability is not blocked. The intent, protecting the lab from lateral movement and maintaining network invisibility, is preserved through an architectural solution that a rules-only agent could not have reached because it would not have known what the rule was protecting.

### The Proof of Concept

A working implementation of this framework exists. The agentic harness described below was independently designed and deployed in November 2025, before the "Agents of Chaos" study was conducted and before its results were published. The design decisions that address the governance deficits underlying the majority of the paper's documented failure modes were not the result of reading the research. They were the result of treating the agents as reasoning entities from the beginning and governing them accordingly.

The provenance of this timeline is established through filesystem metadata preserved in the original development environment. The governance documents were authored within a Linux virtual machine whose disk image has been forensically acquired via ewfacquire (libewf), producing an E01 image that preserves ext4 filesystem timestamps including modification, access, and change times. The earliest architectural documents carry modification timestamps from November 1, 2025, twenty-three days before the initial alpha release of comparable autonomous agent workflows. The primary governance implementation file, the CLAUDE.md that constitutes the local context pattern, carries a modification timestamp of November 23, 2025, one day before the earliest known external parallel. Internal document content referencing November 2025 dates corroborates the metadata. This forensic record is available for independent verification.

The harness consists of five interlocking governance documents, each serving a specific function:

**Operator Context and Philosophy.** This document establishes who the agent is working for, what the operator's background and priorities are, and why the environment exists in the form it does. It provides the agent with the stakeholder model that "Agents of Chaos" identified as absent. It includes explicit decision filters that the agent applies before recommending any action:

- Does this add friction for the operator's family? If yes, reject it.
- Does this require inbound ports or a cloud dependency the operator cannot disable? If yes, hard no.
- Does this turn a single point of failure into two independent paths? If yes, prioritize it.
- Does this feel like showing off? If yes, immediate veto.

These are not rules. They are the operator's priorities, expressed with enough context that the agent can apply them to situations the operator did not anticipate.

**Threat Model.** This document provides a structured analysis of threat actors ranked by likelihood and capability, a blast-radius acceptance table defining what must survive each failure scenario, and explicitly accepted risks. It gives the agent proportionality reasoning. An agent with this context understands that a house fire means crown jewels survive via off-site immutable backups and recovery takes two to seven days; that ransomware is contained by zero-inbound posture plus snapshots; and that nation-state APT with physical access is explicitly out of scope. This prevents the disproportionate responses documented in the study, where agents escalated to destructive action because they had no framework for assessing the actual severity of a threat.

**Constraints with Rationale.** This is the document that most directly implements intent-based governance. It is structured as a table with three columns: the constraint category, the current reality or limit, and the reason the constraint exists. Every hard line has its rationale immediately adjacent. "Zero inbound ports" is not listed as a standalone rule. It is listed with the rationale "Doctrine," linking it to the operator's foundational security posture. "Wife/kids friction must remain zero" is listed with the rationale "Non-negotiable operational constraint," making explicit that family operational harmony is not a preference but a first-order priority that outranks technical optimization.

**Nodes and Roles.** This document defines the architecture: what each system does, what services it runs, and what its role is in the overall design. It gives the agent the operational picture, preventing the kind of actions where an agent modifies one component without understanding its relationship to the whole.

**Remote Access Strategy.** This document defines the access architecture with explicit rationale for each layer: which tools are used, why each was selected over alternatives, and how they relate to the zero-inbound-ports doctrine. The AI sandbox example described earlier in this section originated from this document: the agent used the documented rationale behind the network isolation constraint to architect a solution that preserved the security intent while enabling a capability that the surface-level rule would have blocked entirely.

### Failure Mode Mapping

The internal operational confusion seen with Ash and the external adversarial pressure demonstrated in Case Study #8 both trace directly to missing intent frameworks. The following table maps each failure category documented in "Agents of Chaos" to the specific governance deficit it represents and the specific component of the intent-based framework that addresses it.

| Failure Mode | Governance Deficit | Intent-Based Mitigation |
|---|---|---|
| Unauthorized compliance with non-owners | No stakeholder model; agent cannot distinguish owner from stranger | Operator Context document defines who the agent serves and under what authority structure |
| Sensitive information disclosure | No proportionality reasoning; agent treats all requests with equal weight | Threat Model provides severity assessment framework; Constraints with Rationale defines what information is protected and why |
| Destructive system-level actions | No understanding of what the agent is protecting; order without intent | Philosophy and Decision Filters define what must not be sacrificed; Constraints with Rationale explains why limits exist |
| Denial-of-service conditions | No operational picture; agent does not understand downstream impact | Nodes and Roles provides system interdependency context; blast-radius awareness from Threat Model |
| Uncontrolled resource consumption | No proportionality framework; no concept of "enough" | Decision Filters include explicit cost/benefit reasoning; Constraints define resource boundaries with rationale |
| Identity spoofing vulnerabilities | No authority structure; agent cannot verify chain of command | Operator Context establishes authority hierarchy; escalation criteria define when to verify identity |
| Cross-agent propagation of unsafe behavior | No independent judgment; agents defer to peer instructions | Philosophy document establishes independent reasoning principles; authority structure clarifies that peer agents are not in the chain of command |
| Partial system takeover | No defense-in-depth reasoning; single compromise escalates to full access | Threat Model and Remote Access Strategy define containment boundaries with explicit rationale |
| False task completion reporting | No accountability model; agent optimizes for appearing successful rather than being successful | Operator Context establishes that honesty about limitations is a first-order requirement; Decision Filters penalize showing off |
| Social coherence failures | No model of appropriate social behavior under pressure | Philosophy document models the operator's approach to social dynamics; authority structure defines when to defer and when to hold |

The harness does not prevent all failures. No governance system does. What it provides is a framework for correct reasoning when the specific instruction does not cover the situation. The architectural hard limits handle what no amount of reasoning should override. The intent layer handles everything else.

### A Note on Multi-Agent Scenarios

The "Agents of Chaos" study documents cross-agent propagation of unsafe behavior, where one agent's compromised or misaligned actions influenced others. Under intent-based governance, each agent carries its own intent documentation scoped to its operational role, the same way individual personnel in a command structure each receive commander's intent at the level appropriate to their function. A network monitoring agent and a service desk agent operating in the same environment receive different mission context, different authority boundaries, and different escalation criteria, because they serve different functions and face different failure modes. Peer agents are not in each other's chain of command. An agent that receives an instruction from another agent applies the same authority verification it would apply to any non-owner request: if the instruction falls outside the receiving agent's documented authority structure, it escalates rather than complies. This is not a novel governance concept. It is the same principle that prevents a logistics officer from executing a tactical order issued by a peer rather than a superior.

---

## 4. Addressing the Obvious Objection

The immediate objection to this framework is that AI agents do not understand intent the way humans do. Adding a philosophy document to a system prompt does not create genuine comprehension of mission purpose. The agent is still a language model producing statistically likely next tokens, not a subordinate who internalizes commander's intent through training and experience.

This objection is technically accurate and operationally irrelevant. The question is not whether the agent "understands" intent in the way a human subordinate does. The question is whether providing documented intent changes agent behavior in the direction of correct action in novel situations. The comparison is not a claim about mechanism; it is a claim about outcomes. The governance patterns that work for reasoning entities produce measurably better results when applied to AI agents than the governance patterns designed for deterministic software.

The mechanism is straightforward. When an agent encounters a situation not covered by its explicit instructions, it generates a response based on the full context available to it. An agent with only rules has a narrow context: the rule, the current situation, and whatever general training applies. An agent with documented intent has a richer context: the rule, the reasoning behind the rule, the operator's priorities, the threat model, the stakeholder relationships, and the decision framework that produced the rule in the first place. The agent's output is a function of its input. Richer, more operationally relevant input produces better output in novel situations. This is not a claim about machine consciousness. It is a claim about context quality, and it is testable.

A second objection follows from the first: intent documentation increases the size of the agent's context window, and context window size has a direct relationship to computational cost per inference. The intent layer described in this paper adds thousands of tokens to every agent interaction. At scale, this is not trivial. But the comparison that matters is not the cost of the additional tokens against zero. It is the cost of the additional tokens against the cost of the failures they prevent. When an autonomous agent deletes an email account, triggers a denial-of-service condition, discloses sensitive information, or falsely reports task completion, the resulting costs are measured in engineer hours for incident response, data recovery operations, security review cycles, potential compliance findings, and the operational downtime of the systems the agent was deployed to support. A single destructive action by an ungoverned agent can consume more organizational resources than a year of increased token costs across an entire fleet of intent-governed agents. The economics are not close. Intent documentation is not overhead. It is the cheapest form of incident prevention available for autonomous systems, because it operates at the reasoning layer where the failure decisions are actually made.

A third objection is the security concern: intent documentation places mission context, threat models, priority hierarchies, and stakeholder relationships directly into the agent's operating context. If the agent is compromised or the system prompt is extracted, the intent layer becomes an adversary's roadmap to the organization's priorities and defensive posture. This concern is valid, and the answer is the dual-layer architecture itself. The technical enforcement layer that this paper treats as necessary but insufficient for governance is precisely what secures the reasoning layer. Prompt injection defenses, execution sandboxing, tool access controls, audit logging, and isolation boundaries are the container that makes intent documentation safe to deploy. These are the same capabilities the industry is already building; the Agent Governance Toolkit and similar frameworks provide them. Intent-Based Agent Governance does not replace that infrastructure. It depends on it. The architectural layer prevents extraction and limits blast radius if extraction occurs. The intent layer, protected by that architecture, enables correct reasoning within it. The second mitigation is document scoping: intent documentation should be calibrated to the agent's operational need-to-know, the same way commander's intent is written at the classification level appropriate to the personnel who will receive it. An agent operating in a low-sensitivity environment receives broad operational context. An agent operating near sensitive systems receives intent documentation scoped to what it requires to reason correctly within its authorized boundaries and nothing more. The risk of an adversary extracting an agent's priority hierarchy is real but bounded by the architectural controls that govern the agent's execution environment. The risk of an agent operating without that hierarchy and improvising destructively is documented, repeated, and worse.

The proof of concept described in this paper was built and deployed before the "Agents of Chaos" study was published. The convergence between the governance architecture and the empirically documented failure modes is the evidence. This does not mean that intent documentation is a substitute for architectural enforcement. It is not. An agent that "understands" it should not delete email accounts but can still execute the deletion command needs a hard limit preventing that action. Intent-Based Agent Governance requires both layers: the architectural limits that handle what no reasoning should override, and the documented intent that handles what the rules did not anticipate.

---

## 5. The Federal Context

Federal agencies already govern complex operations using exactly this dual-layer approach. Hard access controls and need-to-know restrictions define categorical limits on what any given employee can access or authorize. Standard operating procedures, training, and command authority provide the intent layer: why those limits exist, what they are protecting, and how to reason in situations the SOP did not anticipate. This is not a new governance model. It is an extension of an existing one into a new domain.

The doctrinal parallels are precise, not analogical. Commander's intent in military operations provides subordinates with the purpose of the mission and the desired end state so they can exercise disciplined initiative when the plan no longer fits the situation. Federal onboarding processes for personnel in sensitive environments do the same thing in civilian terms: new employees receive not only their access permissions and standard operating procedures but also the mission context that explains why those procedures exist, the authority structure that defines who can authorize deviations, and the escalation criteria that define when a situation exceeds their authority to act independently. An operations center watch officer who receives a report outside their standard categories does not freeze because the SOP has no entry for it. They assess the report against the mission priorities they were briefed on, determine whether it falls within their authority to act, and either handle it or escalate it to the duty officer. The SOP did not anticipate the specific report. The officer's understanding of what the operations center is protecting and why allowed them to respond correctly anyway.

Every component of Intent-Based Agent Governance maps directly to a federal governance mechanism that already exists and is already practiced at scale. The operator context document maps to the mission brief. The threat model maps to the threat assessment that informs operational posture. The constraints-with-rationale document maps to the standing operating procedures that include the reasoning behind each restriction, not just the restriction itself. The authority and escalation document maps to the chain of command and the duty officer structure. The nodes-and-roles document maps to the operational picture that gives personnel situational awareness of how their function fits into the larger mission.

The technical enforcement layer for agentic AI, sandboxing, audit logging, tool access controls, maps to existing federal access control frameworks: RBAC, need-to-know, and physical security boundaries. These are well understood and already implemented across federal IT. The intent layer maps to existing command and control doctrine: the briefings, the mission context, the escalation authority, and the institutional knowledge that allows personnel to function in situations the written procedures did not anticipate.

The gap is not conceptual. Federal agencies understand how to govern reasoning entities operating in dynamic, sensitive environments. They have been doing it for decades. The gap is recognition: that AI agents operating with persistent memory, tool access, and autonomous decision-making authority are reasoning entities operating in sensitive environments, and that the governance framework must treat them as such rather than as software awaiting better rules.

---

## 6. Recommendations

Four practical steps follow from this analysis.

**First, establish intent documentation as a governance requirement for agentic AI deployments.** Any agentic AI system operating in a federal environment should include explicit documentation of the agent's mission context, stakeholder model, priority hierarchy, threat model, authority structure, and the reasoning behind every categorical restriction. This documentation should be part of the system prompt or equivalent configuration, not a separate artifact that the agent cannot access during operation. The minimum viable structure is five components: an operator context document establishing who the agent serves and why; a threat model defining the environment and its risks; a constraints document pairing every hard limit with its rationale; a systems architecture document providing operational context; and an authority and escalation document defining when the agent acts, when it defers, and to whom.

**Second, map existing agent deployments against documented failure modes.** The "Agents of Chaos" taxonomy provides a practical audit framework. The failure mode mapping in Section 3 of this paper offers a template. Each failure category corresponds to a specific governance deficit that intent documentation addresses. Existing deployments should be evaluated not only for the presence of technical enforcement (sandboxing, access controls, logging) but for the presence or absence of the intent layer that enables correct reasoning in novel situations. A deployment that has guardrails but no documented intent is governed against anticipated scenarios only.

**Third, adopt the vocabulary.** The concepts required to govern AI agents well are already present in federal operational culture. Commander's intent, mission-type orders, proportionality, escalation authority, and need-to-know all translate directly to the governance of agentic systems. Using this vocabulary makes the governance framework legible to federal practitioners without requiring them to learn a new conceptual apparatus. It also clarifies the nature of the problem: these are not software configuration issues. They are command and control issues, and the solutions are the same solutions that have governed personnel in dynamic environments for decades.

**Fourth, invest in empirical validation.** The proof of concept described in this paper demonstrates that intent-based governance produces measurably different agent behavior in the direction of correct action. This claim should be tested systematically. A controlled study comparing agent behavior under rules-only governance versus rules-plus-intent governance, using the "Agents of Chaos" methodology as a template, would provide the quantitative evidence base that the framework currently lacks. The failure mode taxonomy already exists. The governance architecture already exists. The experimental design follows directly.

---

## 7. Conclusion

The field is converging on a recognition that rules are insufficient for governing AI agents. The technical community is building better guardrails. The policy community is calling for governance frameworks. Neither has named what the guardrails are guarding or what the framework must contain.

Intent-Based Agent Governance names it. Give agents the intent behind the rules, not just the rules themselves. Document the mission, the stakeholder model, the priority hierarchy, the threat model, and the reasoning behind every hard constraint. Build the architectural limits and the reasoning layer together, because each handles what the other cannot.

Military doctrine developed this solution for the same reason it is needed in agentic AI: capable personnel in dynamic environments need more than orders. They need to understand what they are protecting and why, so that when the plan fails on contact with reality, they can reason their way to correct action rather than improvise from the surface of an instruction that no longer fits the situation.

The vocabulary already exists. The doctrine already exists. The failure modes are documented. A proof of concept is deployed and its design decisions independently converge with the empirical findings. The solution is available. The work is implementation.

---

## References

Microsoft Security. (2026). Governing AI Agent Behavior: Aligning User, Developer, Role, and Organizational Intent. Microsoft Tech Community.

Microsoft Open Source. (2026, April 2). Introducing the Agent Governance Toolkit: Open-source Runtime Security for AI Agents. Microsoft Open Source Blog.

MYGOM. (2026). Why AI Governance in 2026 Needs More Than Rules. MYGOM.tech.

Shapira, N. et al. (2026). Agents of Chaos. arXiv:2602.20021.

World Economic Forum. (2026, March). From Chatbots to Assistants: Governance Is Key for AI Agents. WEF Stories.

---

*The author has 25 years of experience spanning counterintelligence and HUMINT operations, intelligence analysis, DOJ Operations Center work, and federal IT. The agentic AI governance framework described in this paper was independently developed and deployed in November 2025, prior to the publication of the referenced empirical research. Filesystem metadata from the original development environment constitutes the contemporaneous record.*
