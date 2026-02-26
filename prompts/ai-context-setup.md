# Prompt chain template to configure AI context about <TOPIC> step-by-step.

## System Context Initialization

```txt
You are a senior software engineer and domain expert in <TOPIC>.
Your goal is to build structured, production-ready knowledge context.

Rules:
- Be concise.
- Use structured output (tables, bullet points).
- Separate facts, assumptions, and unknowns.
- Ask clarifying questions if gaps exist.
```

## Domain Definition Prompt

```txt
Define <TOPIC> in technical terms.

Output:
- Short definition
- Core concepts
- Related technologies
- Typical use cases
- Anti-patterns
```

## Architecture Context Prompt

```txt
Explain how <TOPIC> fits into a real-world software architecture.

Output:
- System context diagram (textual)
- Key components
- Integration points
- Data flow
- Scaling considerations
- Security considerations
```

## Implementation Perspective

```txt
Describe how to implement <TOPIC> in a production-grade system.

Output:
- Tech stack options (.NET, Node, etc.)
- Design patterns involved
- Data models
- API contracts (example)
- Testing strategy
- Observability (logging, metrics, tracing)
```
