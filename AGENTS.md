# Belvedir public docs

This is the public documentation site for **Belvedir** (belvedir.ai), built on [Mintlify](https://mintlify.com). Pages are MDX with YAML frontmatter; configuration lives in `docs.json`. Pushes to `main` deploy automatically via the Mintlify GitHub app, and this site HAS served `docs.belvedir.ai` since Aug 2, 2026; production `platform.belvedir.ai/docs` redirects here.

## Source of truth

The platform repo (`Belvedir/belvedir-platform`) is the source of truth for product behavior: its `src/` route handlers and components, `src/lib/agent-skill.ts` (the agent skill, mirrored to `Belvedir/skills`), `src/app/docs/page.tsx` (the legacy in-app docs page, still served on localhost and previews), `loop/README.md`, `loop-py/README.md`, and its `AGENTS.md` and `docs/agents/*.md`. When integration behavior changes there, this site must be updated to match, in the same change. Never document from memory; open the code and check.

## Terminology (July 2026 Belvedir rename; get this right)

- The product is **Belvedir**; the company is Fractal Machine Research, Inc. Never brand pages "Fractal".
- Packages: npm `belvedir`, PyPI `belvedir` (import `belvedir`). The `@belvedir/loop` and `belvedir-loop` names are supported aliases of the same code; docs should say `belvedir`. The legacy `@fractalresearch/loop` / `fractal-loop` packages still work but are deprecated; mention them only as migration notes.
- API keys start with `bv_live_`; legacy `fr_live_` keys remain valid.
- Env vars are `BELVEDIR_*` (`BELVEDIR_API_KEY`, `BELVEDIR_BASE_URL`, `BELVEDIR_RUN_ID`, `BELVEDIR_TASKS_FILE`); legacy `FRACTAL_*` names are set as aliases in benchmark sandboxes only.
- The ingest default is `https://platform.belvedir.ai`; `platform.fractalresearch.ai` is RETIRED (spans sent there are dropped); see the Common Issues entry.
- Task clusters are **training sets** in all user-facing copy (never "clusters", and no longer "Groups": renamed Aug 10, 2026; the nav page is **Training Sets**). API tokens keep the old name and are contract, not copy: `tier: "group"`, `tier: "group-record"`, `matched_group`, `x-belvedir-group`. Never rewrite those.
- Curation is the **Cleaning log**; projects are **Projects** (never "instances").
- Loop types: **Harness evolution** (whole-repo GEPA), **Prompt evolution** (scaffolding-only GEPA), **LoRA finetuning**. "Memory harness" and version-style loop names ("loop 0.1.0") are retired. NOTE the historical swap: "Prompt evolution" used to mean the whole-repo loop; today it means the scaffolding-constrained one.
- Autonomy (review vs Auto-PR) is chosen **per loop** in the Training setup wizard; there is no project-wide autonomy switch.
- Billing is per **organization** (Organization Settings → Billing); the pay-as-you-go card belongs to the org owner.
- Training compute: never name the managed training backend's vendor. Say **managed fleet** (the default) versus **private GPUs** (Belvedir's own hardware), matching the platform's copy.
- Use the UI's exact control names, bolded: **Token compression** (not "prompt compression" as a control name), **Smart routing**, **Automatic updates**, **Auto reload**, **Chinese models**, **Model training**, **Harness access**, the **Routers** page, the **Cloud Inference** page, **Project Permissions**, **Project settings → Integrations**. Check `src/components/nav.tsx` and the settings components before naming a page or toggle.

## Style preferences

- Use active voice and second person ("you")
- Keep sentences concise: one idea per sentence
- Use sentence case for headings
- Bold for UI elements: Click **Settings**
- Code formatting for file names, commands, paths, and code references
- No em dashes anywhere: prose, tables, code comments, frontmatter. Use a period, comma, colon, semicolon, or parentheses instead. (Copy with em dashes reads as machine-written; this is a house rule across every Belvedir surface.)

## Content boundaries

- Document the public product surface only: the SDKs, the CLI (`cli.mdx`; the CLI talks to one RPC endpoint, `POST /api/v1/cli`, documented through the CLI rather than as a REST surface), dashboard flows, the public API endpoints, and benchmarks/training/routing behavior and pricing.
- The public API endpoints today: `POST /api/v1/traces` (ingest, OTLP JSON or protobuf), `POST /api/v1/outcomes`, `POST /api/v1/route` (routing decision only), `POST /api/v1/route/chat/completions` (OpenAI-compatible inference), `POST /api/v1/route/embeddings`, `/api/v1/route/batches` (create, list, status, results, cancel, plus `/uploads` for large submissions), the Anthropic Messages passthrough `POST /api/v1/messages`, and its batch facade `/api/v1/messages/batches` (create, list, retrieve, results, cancel, delete). Any new public endpoint gets a page or section under `api-reference/` and a line in `api-reference/overview.mdx`.
- Don't document internals: database schema, migrations, worker/optimizer architecture, internal env vars, or admin tooling.
- `sources/` holds scraped reference material, not documentation pages (Mintlify ignores it via `.mintignore`).
