# Supabase and Vercel MCP for the teaching workflow

`.mcp.json` registers two remote MCP servers for compatible agentic IDEs:

- Supabase MCP: `https://mcp.supabase.com/mcp?read_only=true&features=database,docs`
  for inspecting the project and database documentation. Authenticate with the
  Supabase account that owns the intended project.
- Vercel MCP: `https://mcp.vercel.com` for project, deployment, log, and analytics
  context. Authenticate with OAuth when the IDE asks.

MCP is an AI-tool connection. It does not replace the application runtime. The
runtime uses `@supabase/supabase-js` with `SUPABASE_URL` and the server-only
`SUPABASE_SERVICE_ROLE_KEY`. Never put that key in browser code or expose it through
MCP prompts.

## Safe classroom workflow

1. Start with Supabase MCP read-only mode and ask the agent to inspect the project,
   confirm the target project, and explain the app repository’s database migration.
2. Apply the schema through a reviewed SQL migration. Do not ask an agent to drop
   tables or reset a Supabase project.
3. Start the student app and verify its health path, save/list behavior, invalid
   input handling, and persistence in Supabase.
4. Use Vercel MCP to inspect the linked deployment and logs. Require human review
   before changing environment variables, deployments, domains, or production data.

The official Supabase MCP project documents the endpoint and recommends security
best practices. Vercel MCP uses OAuth and grants the connected AI client access
equivalent to the authorized Vercel account, so use a least-privileged account and
confirm mutations explicitly.

If the IDE does not load `.mcp.json`, add the two URLs through its MCP settings.
Do not copy OAuth tokens or Supabase keys into this repository.
