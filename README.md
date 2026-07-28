# Belvedir docs

Public documentation for [Belvedir](https://belvedir.ai), built on [Mintlify](https://mintlify.com). Intended home: `docs.belvedir.ai`.

Pages are MDX with YAML frontmatter; navigation and branding live in `docs.json`. See `AGENTS.md` for terminology rules and the source-of-truth policy (the `Belvedir/belvedir-platform` repo defines product behavior — keep this site in sync with it).

## Local preview

```bash
npm i -g mint
mint dev
```

View at `http://localhost:3000` (run from the repo root, where `docs.json` lives).

## Publishing

Pushes to `main` deploy automatically once the [Mintlify GitHub app](https://dashboard.mintlify.com/settings/organization/github-app) is installed on this repo. Point the `docs.belvedir.ai` domain at Mintlify from the dashboard (Settings → Domain); until then the platform repo's `/docs` page serves that domain.
