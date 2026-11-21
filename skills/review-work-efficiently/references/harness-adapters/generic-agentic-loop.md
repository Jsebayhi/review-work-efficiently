# Harness Adapter: Generic Multi-Agent & API Integration

When integrating into custom LLM harnesses (LangGraph, CrewAI, AutoGen, or direct API calls):

1. **Isolation:** Create a fresh conversation thread for each reviewer with no prior chat history.
2. **Context Quarantine:** Pass only the target artifact and the focus prompt. Never include author chat or internal monologues.
3. **Structured Output:** Enforce a JSON schema requiring:
   - `verdict`: "CLEAN" | "DEFECTS_FOUND"
   - `findings`: Array of objects with `severity` (P0/P1/P2), `location`, `failure_vector`, and `remediation`.
