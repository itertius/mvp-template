# Agentic IDE MVP teaching template

This repository is a documentation-only handbook for teaching assistants and
future AI agents. It does not contain the student application or a runnable
backend. Students create or connect a separate GitHub repository for their MVP.

Start with [skills.md](skills.md), then read [handbook.md](handbook.md). The
lesson sequence is in [docs/sessions.md](docs/sessions.md), MCP guidance is in
[docs/mcp.md](docs/mcp.md), and the deployment blueprint is in
[docs/deployment.md](docs/deployment.md).

The reference delivery path is GitHub → Vercel → Supabase. Supabase MCP helps an
AI assistant inspect and manage the database project; Vercel MCP helps it inspect
deployments. Neither MCP server is an application runtime.

Do not add application source, generated dependencies, environment files, secrets,
database dumps, or deployment state to this repository. Keep service keys in the
student app’s protected Vercel environment variables.
