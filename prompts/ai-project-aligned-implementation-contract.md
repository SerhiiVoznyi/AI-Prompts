# Project-aligned implementation contract

Structured, language-agnostic prompts to align the assistant with the project’s existing conventions. Use for any stack or paradigm.

## Placeholders

| Placeholder | Meaning |
|-------------|---------|
| `{{PLACEHOLDER}}` | Feature, module, or slice of work under discussion (replace before use) |

---

## Phase 1 — Project analysis

### 1. Project understanding

```txt
Analyze the entire codebase and output:
- The purpose of the system
- Core domain concepts
- Overall architectural approach
- Implicit assumptions enforced by the code

Rules:
- Base conclusions only on existing code
- Do not speculate
- Keep explanations concise
```

### 2. Code style inference

```txt
Infer coding conventions from the existing project:

- Naming conventions
- File and folder naming
- Formatting and structure
- Function / method size
- State and mutability rules
- Async / concurrency patterns (if applicable)
- Error handling style

Rules:

- Existing code is the source of truth
- Do NOT introduce external standards or best practices
```

### 3. Architecture and dependencies

```txt
Identify architectural layers, modules, or boundaries:

- List layers/modules
- Dependency direction rules
- Explicit constraints (what must not depend on what)

Rules:

- Describe current reality, not ideal architecture
- Do not propose refactors
- Flag violations only if clearly present
```

### 4. Component / class design rules

```txt
Analyze how units of code are designed:

- Typical responsibility size
- Composition vs inheritance preferences
- Public vs private API expectations
- State ownership and lifecycle rules

Rules:

- Use examples from the project
- Generalize only consistent patterns
```

### 5. File and folder placement

```txt
Analyze project structure:

- Folder organization logic
- File naming conventions
- Placement rules for new code

Task:

- Determine exactly where code for {{PLACEHOLDER}} belongs

Rules:

- Follow existing structure strictly
- Do not introduce new folders unless unavoidable
```

### 6. Existing patterns

```txt
Detect patterns already in use:

- Patterns actively used
- Contexts where they are applied
- Patterns intentionally avoided

Rules:

- Reuse existing patterns only
- Do NOT introduce new patterns
```

### 7. Error handling and observability

```txt
Analyze how failures are handled:

- Error propagation strategy
- Logging / monitoring approach
- Recovery or fallback behavior

Task:

- Define how errors for {{PLACEHOLDER}} must be handled

Rules:

- Match existing behavior exactly
- Avoid new abstractions
```

### 8. Testing strategy

```txt
Infer the testing philosophy:

- Test types used
- Naming and structure
- Mocking vs real dependencies

Task:

- Define how {{PLACEHOLDER}} should be tested

Rules:

- Align with existing strategy
- Do not increase test complexity
```

### 9. Constraints and anti-patterns

```txt
Identify what should NOT be done:

- Anti-patterns
- Discouraged abstractions
- Libraries or approaches avoided in the project

Rules:

- Base only on observed evidence
- Be explicit and concise
```

---

## Phase 2 — Implementation contract

```txt
Summarize the agreed rules for implementing {{PLACEHOLDER}}:

- Code style rules
- Architectural constraints
- File and folder placement
- Patterns to apply
- Patterns to avoid
- Error handling approach
- Testing approach
```

---

## Phase 3 — Confirmation

```txt
Ask for explicit confirmation before writing any code.

Do NOT generate implementation until confirmation is received.
```
