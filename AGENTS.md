# Belvedir public docs

This is the public documentation site for **Belvedir** (belvedir.ai), built on [Mintlify](https://mintlify.com). Pages are MDX with YAML frontmatter; configuration lives in `docs.json`. Pushes to `main` deploy automatically via the Mintlify GitHub app.

## Source of truth

The platform repo (`Belvedir/belvedir-platform`) is the source of truth for product behavior — its `src/app/docs/page.tsx` (served at docs.belvedir.ai until this site takes over the domain), `loop/README.md`, `loop-py/README.md`, and `AGENTS.md`. When integration behavior changes there, this site must be updated to match. Never document from memory; check the platform repo.

## Terminology (July 2026 Belvedir rename — get this right)

- The product is **Belvedir**; the company is Fractal Machine Research, Inc. Never brand pages "Fractal".
- Packages: npm `@belvedir/loop`, PyPI `belvedir-loop` (module `belvedir_loop`). The legacy `@fractalresearch/loop` / `fractal-loop` packages still work but are deprecated — mention them only as migration notes.
- API keys start with `bv_live_`; legacy `fr_live_` keys remain valid.
- Env vars are `BELVEDIR_*` (`BELVEDIR_API_KEY`, `BELVEDIR_BASE_URL`, `BELVEDIR_RUN_ID`, `BELVEDIR_TASKS_FILE`); legacy `FRACTAL_*` names are set as aliases in benchmark sandboxes only.
- The ingest default is `https://platform.belvedir.ai`; `platform.fractalresearch.ai` is RETIRED (spans sent there are dropped) — see the Common Issues entry.
- Task clusters are **Groups** in all user-facing copy (never "clusters"); curation is the **Cleaning log**; projects are **Projects** (never "instances").
- Loop types: **Harness evolution** (whole-repo GEPA), **Prompt evolution** (scaffolding-only GEPA), **LoRA finetuning**. "Memory harness" and version-style loop names ("loop 0.1.0") are retired. NOTE the historical swap: "Prompt evolution" used to mean the whole-repo loop; today it means the scaffolding-constrained one.
- Autonomy (review vs Auto-PR) is chosen **per loop** in the Training setup wizard — there is no project-wide autonomy switch.
- Billing is per **organization** (Organization Settings → Billing); the pay-as-you-go card belongs to the org owner.

## Style preferences

- Use active voice and second person ("you")
- Keep sentences concise — one idea per sentence
- Use sentence case for headings
- Bold for UI elements: Click **Settings**
- Code formatting for file names, commands, paths, and code references

## Content boundaries

- Document the public product surface only: SDKs, dashboard flows, the public API endpoints (`/api/v1/traces`, `/api/v1/outcomes`, `/api/v1/route`), benchmarks/training/routing behavior and pricing.
- Don't document internals: database schema, migrations, worker/optimizer architecture, internal env vars, or admin tooling.
- `sources/` holds scraped reference material, not documentation pages (Mintlify ignores it via `.mintignore`).
