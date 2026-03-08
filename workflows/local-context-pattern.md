# Local Context Workflow for Claude Code

## Problem Statement
I set out to evaluate whether Claude, Gemini, and Grok could provide Project-level
functionality while maintaining complete data sovereignty — no persistent cloud storage,
only API calls exposed to external services.

## Methodology
- I created a local directory structure mirroring the web UI Project
- I loaded existing documentation without pre-structure
- I used the `/init` command to generate a CLAUDE.md context file
- I tested across multiple sessions for context persistence
- I compared effectiveness against the web UI Projects feature

## Results
- Achieved functional equivalence to cloud-based Projects
- All context stored locally in human-readable CLAUDE.md
- Zero server-side persistence beyond API request/response
- Portable across systems via simple directory copy
- Full audit trail via filesystem operations

## Trade-offs
- Requires directory navigation before starting Claude Code
- Device-dependent access (mitigated via Nextcloud sync or rsync+cronjob)
- Manual backup/version control responsibility
- No cross-device automatic synchronization

## Key Finding
Projects/persistent memory are primarily UI conveniences. Core AI capability operates
effectively with filesystem-based context management.

## Implications
- **Federal/IC environments (with self-hosted LLM):** Viable deployment pattern for
  classified systems using local models — eliminates need for user profile databases
  on the LLM server, keeping it stateless and reducing attack surface. All context
  lives on user workstations at appropriate classification levels.
- **Compliance-heavy industries:** Meets data residency requirements with full audit trail
- **Individual users:** Complete control over AI interaction data
- **Enterprise adoption:** Blueprint for on-premises AI integration without complex
  user data management

## Technical Requirements
- LLM CLI access
- Local filesystem
- Sync solution for multi-device access (optional)

## Pattern Applicability
I tested this workflow with Claude Code, but the pattern is deployment-agnostic — it
works equally well with self-hosted models like LLaMA, Mistral, or government-approved
LLMs in air-gapped environments.

## Next Steps
- Validate with security
- Identify pilot use case
- Document deployment pattern
