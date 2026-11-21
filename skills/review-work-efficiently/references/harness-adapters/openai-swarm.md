# Harness Adapter: OpenAI Swarm & Operator

In Swarm or Operator multi-agent architectures:

```python
from swarm import Agent

def create_adversarial_agent(focus_name, focus_instructions):
    return Agent(
        name=focus_name,
        instructions=f"{focus_instructions}\nStrict Proof-of-Failure contract enforced.",
        functions=[]  # Strictly read-only or no mutation functions
    )
```
