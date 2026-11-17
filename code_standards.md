# Code standards

## General

1. Keep it simple, do not overcomplicate.
2. Comments only when necessary.
3. Be concise: a short README and no decorative emojis. Only these status symbols are allowed, and only where they show state, such as test results, logs and feature status: ✅ done or passing, ❌ failed, ⏳ waiting or in progress, ⚠️ needs attention.
4. IMPORTANT: avoid overly defensive code. Handle exceptions only when necessary.
5. Use uv: ALWAYS `uv run`, NEVER `python3`.
6. TypeScript: strict mode, never `any`.
7. Every project creates its own `BRAND.md` with its own fonts, colors and rules. Nothing branded is hardcoded outside it.
8. Every project has an `AGENTS.md` at the root. It is the first file an agent reads: a short map of what the project is and where everything lives, pointing to `PROJECT_RULES.md`, the standards files and `CODE_INDEX.md`.
9. README: one screen, with six parts. The project name and a one-line description. Setup: the exact commands, such as `uv sync` and copying `.env.example` to `.env`. How to run it, with one command to start everything. How to run the tests. A short map of the folders. A pointer saying to read `AGENTS.md` first. Leave out long explanations, feature lists and anything that duplicates `docs/`, `FEATURES.md` or `CODE_INDEX.md`.

## Naming and style

1. Python uses snake\_case for functions and variables, PascalCase for classes, UPPER\_CASE for constants.
2. SQL and dbt models use snake\_case with prefixes: `stg_` for staging, `fct_` and `dim_` for marts.
3. Format with Black and lint with Ruff.

## Code structure

1. Small functions that each do one job.
2. Type hints on every Python function signature.
3. No duplicated logic, but extract a helper only when something is used in a third place.
4. One clear purpose per module.

## Function comments and code index

1. Every function gets a short docstring, one or two lines, saying what it does and why it exists. No comments on obvious code.
2. Keep `CODE_INDEX.md` at the project root. Before writing a function, read the index to check it does not already exist.
3. A script generates the index from the docstrings, organized by structure: each file is a section, classes sit under their file, and methods sit under their class, each with its what-and-why line.
4. Never edit the index by hand. Run the script after adding or changing a function.
5. Every function in the index has a stable, versioned id made from its file, its name and a version, such as `claims.pay_claim_v1_0`. Bump the version whenever the function's behavior changes: a small change goes from `v1_0` to `v1_1`, a breaking change from `v1_1` to `v2_0`. The id shows in the docstring and the index.
6. Keep `FEATURES.md` at the project root. Each feature has one line, a version, a status (planned, in progress or done), and the versioned ids of the functions that implement it. Keep a changelog at the end with one line per change: date, feature, version, and what changed. Update the file whenever a feature is added or changed.

## Testing

1. Workflow for every language and tool: Design, Implement, Unit Test, Process Test, Crash Test, Regression Test, Validate, Report. Implement and Unit Test run as a loop: test each function right after writing it.
2. Design: write a short plan before coding. Unit test: test each function on its own. Process test: run the whole flow end to end. Crash test: feed bad input, missing data and failing services, and confirm it fails clearly. Regression test: rerun the full suite after every change, and run everything before calling anything done. Validate: check the result against the original request, not only against passing tests. Report: a short summary of what changed, what passed and what is still open.
3. Tools: pytest for Python, run with `uv run pytest`. Playwright for end-to-end. For any new language or tool, use its standard test framework and follow the same workflow.
4. Test behavior, not implementation: cover the main path and the obvious failure cases, and skip trivial getters. For data work, check row counts, nulls on key columns, and duplicates after each transformation.

## Error handling and logging

1. Fail loudly: no empty except blocks, and never swallow an exception silently.
2. Handle errors only at boundaries, like API inputs, file reads and calls to outside services. Let everything else propagate.
3. Error messages say what failed and with which input.
4. Error logs answer three things: what failed, where it happened (function or file), and how (key inputs such as a claim id, the error message and the full trace). Logging is separate from handling: handling decides what the code does, logging records what happened.
5. Every run logs a clear start and a clear end with a status, success or failed, and the reason if it failed.

## Config and secrets

1. No hardcoded values: anything that changes between environments, like keys, URLs and model names, comes from environment variables.
2. Secrets live in `.env`, which is always in `.gitignore`. Never put secrets in code, logs or commits.
3. Keep a `.env.example` with the variable names and no real values.
4. Fail fast at startup if a required variable is missing, with a message naming it.

## Git and commits

1. Small commits: each commit does one thing, so any change is easy to find and undo.
2. Commit messages: a short summary line in the present tense, such as "Add claim payment endpoint", plus a line of why if it is not obvious.
3. Never commit secrets, `.env` or other generated files. The exception is `CODE_INDEX.md`: commit it together with the code change that updated it.

## Branches

1. One short-lived branch per change, such as `feature/claim-payment`.
2. Build and test on the branch, merge to main only when the full suite passes, then delete the branch.
3. No permanent testing branch, so main always stays working.

## Dependencies

1. Add a package only when really needed. Prefer the standard library or a small package over a heavy one for a small job.
2. Manage Python dependencies with uv in the single root `pyproject.toml`. Commit the lock file so builds are repeatable.
3. Pin versions, and remove a dependency as soon as it is no longer used.
