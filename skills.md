# Teaching assistant agent guidance

This repository is documentation-only. It contains the operating instructions for
future AI assistants and TAs; it intentionally does not contain an application,
Docker stack, database credentials, or deployment artifacts.

## Required reading

1. Read this file before planning work.
2. Read [README.md](README.md) for the repository contract.
3. Read [handbook.md](handbook.md) for TA practice and [docs/sessions.md](docs/sessions.md)
   for the lesson sequence.
4. Read [docs/mcp.md](docs/mcp.md) before using Supabase or Vercel MCP.
5. Read [docs/deployment.md](docs/deployment.md) before proposing a deployment.

## Repository contract

- Do not assume source code exists here. A student application belongs in a
  separate project repository created during the workshop.
- Keep this repository limited to Markdown guidance. Do not add generated code,
  `.env` files, service keys, Docker files, database dumps, or node modules.
- User instructions take precedence over this guidance. State assumptions when
  a target app, Supabase project, GitHub repository, or Vercel project is missing.
- Never claim an app is deployed or tested without a real URL and command output.

## Teaching workflow

For each task, use: **context → acceptance → smallest change → inspect → verify →
explain**.

Ask the student to state the target user, problem, and one observable behavior.
Have the agent inspect the student’s application repository before editing. Keep
the MVP to one audience, one problem, and one primary workflow. Review every diff,
test both success and invalid input, and explain the result in plain language.

When a failure occurs, capture the exact command, response, and relevant log;
rank likely causes; change one responsible layer; and rerun a focused check. Do
not blindly reinstall, reset a database, delete a Vercel deployment, or rewrite
the application.

## Intended reference architecture

The workshop’s reference stack is:

- GitHub: source control, pull requests, and checks.
- Vercel: frontend and serverless API deployment.
- Supabase: managed Postgres and project migrations.
- Supabase MCP: database and project inspection for the AI assistant.
- Vercel MCP: deployment and project inspection for the AI assistant.

MCP is an agent connection, not the application runtime. Supabase service-role
keys belong only in server-side Vercel environment variables. They must never be
placed in browser code, Markdown, GitHub, or an MCP prompt.

## Verification

For a student application, verify the repository’s own checks, then verify the
deployed URL: health endpoint, primary workflow, invalid input, and persistence.
For Supabase changes, inspect the migration and confirm the intended project before
applying it. For Vercel changes, review the preview deployment and require human
confirmation before production, environment, domain, or data mutations.

This repository is complete when a future agent can follow these documents without
mistaking the handbook for runnable application code.
