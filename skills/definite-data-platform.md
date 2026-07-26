---
name: Operate the Definite data platform via MCP
description: >-
  Query data, manage the semantic layer, connect integrations, configure syncs,
  and build dashboards in Definite through its native Model Context Protocol
  server. Mirrors the official published skill at
  github.com/definite-app/claude-skills.
api: mcp/definite-mcp.yml
published: https://github.com/definite-app/claude-skills
method: searched
operations:
- run_sql_query
- run_cube_query
- list_cube_models
- save_cube_model
- create_integration
- list_integrations
- configure_sync
- list_sync_runs
- create_doc
- update_doc
- execute_doc
- read_drive_file
- write_drive_file
---

# Operate the Definite data platform via MCP

Definite speaks the Model Context Protocol natively. Connect the server, then use
its 40+ tools (six categories) to run an entire data platform from an agent.

## Connect

Add the hosted HTTP MCP server (see `mcp/definite-mcp.yml`):

```
claude mcp add definite --transport http https://api.definite.app/v3/mcp/http \
  --header "Authorization: YOUR_API_KEY"
```

Auth is a bearer API key from the bottom-left user menu in the Definite app, or
OAuth 2.1 (authorization-code + PKCE, scope `mcp`) per
`https://api.definite.app/.well-known/oauth-authorization-server`.

## Query data

- `run_sql_query` — execute raw SQL against the DuckDB / DuckLake warehouse.
- `run_cube_query` — pull governed metrics from the semantic layer for
  consistent definitions across the organization.

## Manage the semantic layer

- `list_cube_models` — inspect existing Cube metric/model definitions.
- `save_cube_model` — create or update a semantic model so metrics stay
  consistent everywhere.

## Connect sources and configure syncs

- `create_integration` / `list_integrations` — connect and review data sources
  (500+ managed connectors).
- `configure_sync` / `list_sync_runs` — set up pipelines and monitor sync runs.

## Build dashboards

- `create_doc` / `update_doc` / `execute_doc` — build, edit, and run Definite
  Docs (dashboards, reports, data apps).

## Files

- `read_drive_file` / `write_drive_file` — read and write files in Definite Drive.

## Conventions

- All calls authenticate with the bearer API key or MCP OAuth token above.
- The REST surface is versioned in the URL path (`/v1` REST, `/v3` MCP,
  `/v4` webhooks) — see `conventions/definite-conventions.yml`.
- No idempotency-key, pagination, or rate-limit contract is documented publicly;
  do not assume one.
