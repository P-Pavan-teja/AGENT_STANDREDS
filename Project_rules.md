# Project rules

Template. Fill in the values for each project. If anything here conflicts with the common files, this file wins.

## Overview

Two or three lines: what the project is, who it is for, and what done looks like.

## Common files

This project follows `docs/CODE_STANDARDS.md`, `docs/TECH_STACK.md` and its own `docs/BRAND.md`.

## Project setup

When a project starts, create exactly this structure. Nothing more.

### Mandatory

```
project/
  AGENTS.md
  README.md
  CODE_INDEX.md
  FEATURES.md
  pyproject.toml
  uv.lock
  .python-version
  .env.example
  .gitignore
  docs/
    PROJECT_RULES.md
    CODE_STANDARDS.md
    TECH_STACK.md
    BRAND.md
  scripts/
```

### Optional, created only when the project needs it

```
  backend/     when the project has an API
  agent/       when it uses an LLM agent
  dashboard/   when it has a frontend
  e2e/         when there is a dashboard to test
  data/        when it starts from business data
```

### Setup rules

1. Create all mandatory files and folders first, in the layout above.
2. Create an optional folder only when its condition is true.
3. Do not create empty placeholder folders.
4. Do not create any folder or file that is not on this list. If something new seems necessary, ask first.
5. Fill `docs/BRAND.md` with this project's own fonts, colors and tone before any UI work.
6. Add the code index script to `scripts/`, then generate `CODE_INDEX.md`.

## Project-specific rules

- &#91;What the agent can and cannot touch.\]
- &#91;Data it must never see.\]
- &#91;Any override of the common files, such as a different database or an extra tool.\]

## How to run and test

- Start locally: \[command\]
- Run the tests: \[command\]
- Rebuild the code index: \[command\]
