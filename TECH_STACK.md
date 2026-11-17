# Tech stack

## Backend

1. Use FastAPI with Uvicorn only when a project exposes an API, such as for a dashboard or an agent. Skip it for pipelines and scripts with no endpoints.
2. Every API operation has an `operation_id`, a one-line docstring and no optional inputs.
3. Validate inputs and outputs with Pydantic.
4. Start with SQLite as the database.

## Language and tooling

1. Python 3.12 with uv, all in the root `pyproject.toml`.
2. Node 26 for any frontend work.
3. The OpenRouter key is `OPENROUTER_API_KEY` in `.env`.
4. Pin the Python version in a `.python-version` file. Add packages with `uv add` and commit `uv.lock`. On a fresh clone, run `uv sync` so Mac and Windows get identical environments.

## Agents

1. Use LangChain's `create_agent` on OpenRouter, with the key in `.env`.
2. One entry point per agent, taking an id and a thread id.
3. The agent reaches data and instructions only through the backend API, never directly.
4. The model comes from the `MODEL_NAME` environment variable, with a default, so models can be swapped without touching code.
5. Match reasoning effort to the task, set per agent through an environment variable. Low is the default, for simple steps like tool calls and lookups. Medium for tasks that need judgment or multi-step planning. High only for hard problems like complex analysis.

## Dashboard

1. React with Vite and TypeScript, in strict mode.
2. The dashboard talks to the backend only through its API, never to the database directly.
3. Playwright for end-to-end tests, run with a single command.
4. Styling follows the project's own `BRAND.md`. Fonts, colors and surfaces come from there, nothing hardcoded.

## UI

1. It must look human-made, not generic AI output: no single flat page of text and cards to scroll through.
2. Use a real app layout: a sidebar or top navigation, with a separate page for each area.
3. Mix content types in each view: tables, charts, filters and detail views, not walls of text.
4. Give it visual hierarchy and personality, with the brand's accent colors doing real work.
5. Avoid the AI giveaways: no centered hero blurbs, no grids of identical icon cards, and no gradient fills.
6. Use real controls: tabs to split related views, toggles for on and off settings, and buttons for clear actions with one primary button per screen.
7. Use dropdowns and filters to narrow data, a search box on long lists, and sortable tables.
8. Use modals only for quick confirmations.
9. Every screen handles loading, empty and error states.
10. Responsive on desktop and mobile, with readable contrast.

## Orchestration

1. Use Airflow for orchestration: scheduling, ordering and retrying multi-step jobs.

## Folder layout

1. Each folder has one job, so the top level shows what the project does.
2. Root folders: `backend/`, `agent/`, `dashboard/`, `e2e/` for end-to-end tests, `data/`, `scripts/` for helper scripts, and `docs/`. Include only the ones a project needs.
3. Root files: `AGENTS.md` as the front door, a short `README.md`, `CODE_INDEX.md`, FEATURES.md, `pyproject.toml`, `uv.lock`, `.python-version`, `.env.example` and `.gitignore`.

   `docs/` holds the project's rule files: `PROJECT_RULES.md`, `CODE_STANDARDS.md`, `TECH_STACK.md` and `BRAND.md`. `AGENTS.md` links to each by path, so nothing is missed.
4. Inside `backend/`, split by responsibility, not by file type: API routes, business logic, database access and schemas each get their own place. A `tests/` folder mirrors the same structure.
5. Inside `dashboard/`, keep pages, components and the API client in separate folders.
6. `data/` holds the business data the backend starts from. The agent never sees `data/evals/`, which holds the answer key.
7. Avoid a dumping-ground `utils` folder, one giant main file, and folders named after tools instead of purpose.
8. Leave no demo clutter: no sample, temp or scratch files committed.

## Cross-platform

1. Everything must run on both Mac and Windows.
2. Use `pathlib` for file paths, never hardcoded slashes.
3. Write helper scripts in Python and run them with `uv run`, not in shell-specific scripts.
4. Test on both Mac and Windows before release.
