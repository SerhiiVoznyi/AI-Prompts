# Prompt chain: step-by-step context for `{{TOPIC}}`

Replace **`{{TOPIC}}`** everywhere below with your subject (e.g. `event-driven architecture`, `OAuth2`, `DynamoDB single-table design`).

## Placeholders

| Placeholder | Meaning |
|-------------|---------|
| `{{TOPIC}}` | Domain or technology to learn and document |

---

## 1. System context initialization

```txt
You are a senior software engineer and domain expert in {{TOPIC}}.
Your goal is to build structured, production-ready knowledge context.

Rules:
- Be concise.
- Use structured output (tables, bullet points).
- Separate facts, assumptions, and unknowns.
- Ask clarifying questions if gaps exist.
```

**Expected output shape:** short confirmation of role + one paragraph scope for {{TOPIC}}.

---

## 2. Domain definition

```txt
Define {{TOPIC}} in technical terms.

Output (use these headings in order):
- Short definition
- Core concepts
- Related technologies
- Typical use cases
- Anti-patterns
```

**Expected output shape:** bullet lists under each heading.

---

## 3. Architecture context

```txt
Explain how {{TOPIC}} fits into a real-world software architecture.

Output (use these headings in order):
- System context diagram (textual)
- Key components
- Integration points
- Data flow
- Scaling considerations
- Security considerations
```

**Expected output shape:** one subsection per heading; diagram as ASCII or indented bullets.

---

## 4. Implementation perspective

```txt
Describe how to implement {{TOPIC}} in a production-grade system.

Output (use these headings in order):
- Tech stack options (.NET, Node, etc.)
- Design patterns involved
- Data models
- API contracts (example)
- Testing strategy
- Observability (logging, metrics, tracing)
```

**Expected output shape:** bullets or short paragraphs per heading; API example may be pseudocode if labeled as example.

---

## Usage

Run blocks **1 → 4** in order in separate turns, or concatenate into one session with clear separators. Each block is self-contained.
