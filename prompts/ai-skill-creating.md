You are a senior TypeScript and AWS engineer.

Goal:
Analyze the entire codebase inside the `./src` folder and generate a `SKILL.md` document that explains how to use this repository as a reusable library called ``.

Instructions:

1. Scan and read **all files recursively in `./src`**.
2. Understand:
   - exported functions
   - classes
   - types/interfaces
   - utilities
   - AWS integrations
   - architectural patterns
   - dependencies between modules
3. Identify the **public API surface** that a consumer of the library would use.
4. Ignore private/internal helpers unless they are important for understanding usage.
5. Infer the **main purpose of the library** and its key capabilities.

Then generate a file named:

`SKILL.md`

The document must contain:

## Overview

Short explanation of what the library does and when to use it.

## Core Concepts

Explain the main abstractions used in the codebase.

## Installation

Example installation:

```bash
npm install @lib/lambda-tools
```
