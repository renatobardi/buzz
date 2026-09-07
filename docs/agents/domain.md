# Domain Docs

How the engineering skills should consume this repo's domain documentation when exploring the codebase.

## Before exploring, read these

- **`CONTEXT-MAP.md`** at the repo root — it points at one `CONTEXT.md` per context. Read each one relevant to the topic.
- **`docs/adr/`** — system-wide decisions. Also check `<context>/docs/adr/` for context-scoped decisions (e.g. `crates/buzz-relay/docs/adr/`, `desktop/docs/adr/`).

If any of these files don't exist yet, **proceed silently**. Don't flag their absence; don't suggest creating them upfront. The `/domain-modeling` skill (reached via `/grill-with-docs` and `/improve-codebase-architecture`) creates them lazily when terms or decisions actually get resolved.

## File structure

This repo is multi-context (`CONTEXT-MAP.md` at the root). Contexts follow the existing product surfaces in [AGENTS.md § Repo Structure](../../AGENTS.md#repo-structure) — natural boundaries are the relay/backend crates (`buzz-relay`, `buzz-core`, `buzz-db`, `buzz-auth`, `buzz-pubsub`, `buzz-search`, `buzz-audit`, `buzz-media`), the agent surface (`buzz-acp`, `buzz-agent`, `buzz-dev-mcp`, `buzz-persona`, `buzz-workflow`), the CLI (`buzz-cli`, `buzz-sdk`, `buzz-admin`), and each client app (`desktop/`, `web/`, `admin-web/`, `mobile/`). Don't force a `CONTEXT.md` per crate — group crates that share one bounded context, split further only when their vocabularies actually diverge.

```
/
├── CONTEXT-MAP.md
├── docs/adr/                          ← system-wide decisions
├── crates/
│   ├── buzz-relay/
│   │   ├── CONTEXT.md
│   │   └── docs/adr/                  ← relay-specific decisions
│   └── buzz-cli/
│       ├── CONTEXT.md
│       └── docs/adr/
├── desktop/
│   ├── CONTEXT.md
│   └── docs/adr/
├── mobile/
│   ├── CONTEXT.md
│   └── docs/adr/
└── web/
    ├── CONTEXT.md
    └── docs/adr/
```

## Use the glossary's vocabulary

When your output names a domain concept (in an issue title, a refactor proposal, a hypothesis, a test name), use the term as defined in the relevant context's `CONTEXT.md`. Don't drift to synonyms the glossary explicitly avoids.

If the concept you need isn't in the glossary yet, that's a signal — either you're inventing language the project doesn't use (reconsider) or there's a real gap (note it for `/domain-modeling`).

## Flag ADR conflicts

If your output contradicts an existing ADR, surface it explicitly rather than silently overriding:

> _Contradicts ADR-0007 (event-sourced orders) — but worth reopening because…_
