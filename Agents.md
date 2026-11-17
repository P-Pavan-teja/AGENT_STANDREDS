# Agents

Template. Keep it short: this file is a map, not a manual. Fill in the values for each project.

## Project

&#91;One or two lines: what this project is and who it is for.\]

## Read first

1. Read docs/`PROJECT_RULES.md` first. It holds the rules specific to this project, and it wins if anything conflicts with the common files.
2. Then follow the common files below.

## Where everything is

- `docs/PROJECT_RULES.md`: this project's overview, rules, overrides, and how to run and test it.
- `docs/CODE_STANDARDS.md`: how code is written, tested, logged, committed and branched.
- `docs/TECH_STACK.md`: the tools, folder layout and defaults.
- `docs/BRAND.md`: this project's fonts, colors and tone.
- `CODE_INDEX.md`: every function and class, organized by file, with what it does and why it exists.
- `FEATURES.md`: every feature with its version, status and the versioned ids of the functions that implement it, plus a changelog.

## Before you write code

1. Check `CODE_INDEX.md` to see whether the function already exists.
2. After adding or changing a function, run the index script and commit the updated index with your change.

## Never

- &#91;Anything this project's agent must never touch or see, such as a folder or a data set.\]
