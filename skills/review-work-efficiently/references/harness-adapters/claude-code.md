# Harness Adapter: Claude Code / Anthropic Subagents

In Claude Code or Anthropic-based harnesses, dispatch sub-agents using your native sub-agent or task spawning primitives:

```markdown
Use your sub-agent tool to dispatch an isolated task:
- Subagent Role: "Test Suite Auditor"
- Context: Send ONLY the changed diff and the Focus 2 instructions.
- Tool Permissions: Read-only (Read files, search, view). Forbid edit or bash execution.
- Directive: Enforce Proof-of-Failure mandate. Return JSON findings or NO_FAILURES_FOUND.
```
