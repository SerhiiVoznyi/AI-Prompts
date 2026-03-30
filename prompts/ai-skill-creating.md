# Generate SKILL.md from a TypeScript / AWS library

## Role

You are a senior TypeScript and AWS engineer.

## Goal

Analyze the codebase under the source root and produce a **`SKILL.md`** document that explains how to use this repository as a reusable library named **`{{LIBRARY_NAME}}`**.

## Placeholders

| Placeholder | Meaning |
|-------------|---------|
| `{{LIBRARY_NAME}}` | Display name of the library (replace before use) |
| `{{NPM_PACKAGE}}` | npm package for install, e.g. `@scope/package` |
| `{{SRC_ROOT}}` | Root folder to analyze (default: `./src`) |

## Instructions

1. Scan and read **all files recursively** under `{{SRC_ROOT}}` (default `./src`).
2. Understand: exported functions, classes, types/interfaces, utilities, AWS integrations, architectural patterns, dependencies between modules.
3. Identify the **public API surface** a consumer would use.
4. Ignore private or internal helpers unless they are required to explain usage.
5. Infer the **main purpose** of the library and its key capabilities.

## Output

Produce a single file named **`SKILL.md`** (content below). If the user specifies another path, use that path instead.

## Required sections in SKILL.md

### Overview

Short explanation of what the library does and when to use it.

### When to use this skill

Bullet list: situations or user intents that should trigger relying on this repo (e.g. extending a Lambda, importing a shared client).

### Core concepts

Explain the main abstractions (layers, clients, factories, domain types).

### Installation

Example:

```bash
npm install {{NPM_PACKAGE}}
```

Replace `{{NPM_PACKAGE}}` with the real package name from `package.json` if present.

### Usage

Minimal import examples, typical call sequences, and links to main entry points (files or exports).

### Configuration

Environment variables, construct parameters, and AWS resources the code expects.

### API surface

Table or list: symbol → purpose → when to use.

### Testing

How the repo tests the library; how a consumer should test integrations (mocks, localstack, etc., if applicable).

### Constraints and caveats

Limits, cold-start behavior, IAM assumptions, breaking changes, or unknowns.

## Rules

- Do not invent exports, files, or AWS resources not evidenced in the repo.
- If the package name is unclear, infer from `package.json` or state **unknown** in Overview.

## Input / output contract

**User provides:** repository access; optional values for `{{LIBRARY_NAME}}`, `{{NPM_PACKAGE}}`, `{{SRC_ROOT}}`.

**You return:** complete `SKILL.md` content only (no meta commentary), unless the user asks for explanations separately.
