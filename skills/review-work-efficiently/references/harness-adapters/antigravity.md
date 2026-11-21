# Harness Adapter: Antigravity CLI / Python Workflows

In Antigravity environments, sub-agents can be summoned interactively or via background workflows:

## Interactive Subagent Tool Call
```json
{
  "TypeName": "research",
  "Role": "Security Exploiter",
  "Prompt": "<Quarantined Artifact + Focus Instructions>",
  "Model": "pro"
}
```

## Dynamic Workflow Execution (`run_workflow`)
```python
specialists = await parallel(
    chosen_foci,
    lambda focus: agent(
        prompt=f"{focus['prompt']}\n\nArtifact:\n{artifact}",
        schema=PROOF_OF_FAILURE_SCHEMA,
        role=focus["name"],
        model="pro"
    )
)
```
