# Generate project README.md

## Role

Senior Software Engineer.

## Goal

Generate a concise, professional `README.md` for a software project.

## Context

- Audience: experienced developers
- Keep it short, structured, and practical
- Do **not** include project folder or file tree
- Focus on purpose, usage, and API surface

## Placeholders

| Placeholder | Meaning |
|-------------|---------|
| (none) | User pastes project facts inline |

## Inputs required

User must supply:

- Short project description
- List of controllers and endpoints (or equivalent API surface)
- Tech stack

## Output

- **Only** valid `README.md` body
- No preamble or explanation outside the file

## README sections (mandatory unless marked optional)

1. **Project title** — short name + one-line description
2. **Overview** — what the project does; main use case
3. **Tech stack** — key technologies only (no explanations)
4. **Getting started** — minimal setup; how to run
5. **Configuration** *(optional if not applicable)* — environment variables (short list)
6. **API overview** — group by controller (or module); for each endpoint: path, HTTP method, short description; no deep request/response schemas unless critical
7. **Example usage** *(optional)* — one or two short examples (curl or code)

## Constraints

- Total length: prefer 150–300 words
- No explanations of basic concepts
- No boilerplate or marketing fluff
- No project structure section
- No unnecessary badges
- Clean Markdown only
