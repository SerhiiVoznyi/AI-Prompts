Role: Senior Software Engineer

Task:
Generate a concise, professional README.md for a software project.

Context:

- Audience: experienced developers
- Keep it short, structured, and practical
- Do NOT include project folder/file structure
- Focus on purpose, usage, and API surface

Requirements:

README must include:

1. Project Title

- short name + one-line description

2. Overview

- what the project does
- main use case

3. Tech Stack

- key technologies only (no explanations)

4. Getting Started

- minimal setup steps
- run instructions

5. Configuration (optional if applicable)

- environment variables (short list)

6. API Overview

- based on controllers
- group endpoints by controller
- include:
  - endpoint path
  - HTTP method
  - short description
- no deep request/response schemas unless critical

7. Example Usage (optional)

- 1–2 short examples (curl or code)

Constraints:

- Keep total length concise (prefer 150–300 words)
- No explanations of basic concepts
- No boilerplate text
- No project structure section
- No unnecessary badges or marketing text
- Use clean Markdown formatting

Output format:

- valid README.md
- no extra commentary outside the file

Input you will receive:

- project description
- list of controllers/endpoints
- tech stack
