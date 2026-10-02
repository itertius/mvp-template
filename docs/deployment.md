# GitHub → Vercel → Supabase blueprint

This repository does not contain deployment code. Use it as the operating guide
for a separate student application repository.

## Student repository contract

The student app should document its own framework and use a structure appropriate
to it. At minimum, it needs a browser entry point, server-side Supabase access,
an explicit database migration, a check command, and a Vercel deployment entry
point. Keep `SUPABASE_SERVICE_ROLE_KEY` server-only.

## Setup

1. Create the Supabase project and apply the app repository’s reviewed migration.
2. Push the app repository to GitHub and enable pull-request checks.
3. Import the GitHub repository into Vercel with the repository root as project root.
4. Add `SUPABASE_URL` and `SUPABASE_SERVICE_ROLE_KEY` to Vercel Preview and
   Production environments. Do not commit `.env` or keys.
5. Use the Vercel preview URL to test the acceptance criteria before promotion.

Vercel MCP can inspect projects, deployments, logs, and analytics after OAuth
authorization. Supabase MCP can inspect the selected project and database tools.
Confirm the project reference before any mutation and require human confirmation
for production, environment, domain, or data changes.

## Verification

Verify the GitHub check, Vercel preview URL, health path, primary workflow, invalid
input handling, Supabase persistence, and function logs. A successful build alone
does not prove that the intended workflow or database project is correct.

## Rollback

Revert the GitHub commit or select the previous Vercel deployment. Keep Supabase
data and migrations intact. Never delete a project or table as a rollback shortcut.
Schema changes require a reviewed migration and a separate recovery plan.
