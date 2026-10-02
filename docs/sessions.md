# Session outline

The template itself is documentation-only. Each team brings a separate GitHub
application repository. Use the same four outcomes whether the app is built with
Next.js, another Vercel-supported framework, or a small serverless API.

## Session 1 — Problem and repository orientation

Outcome: one target user, one problem, one primary workflow, and three acceptance
criteria. The student attaches `skills.md` and asks the agent to inspect the app
repository before proposing changes.

Prompt: “Inspect the existing application and explain its UI, API, Supabase access,
and deployment entry points. Do not edit files. Propose the smallest workflow for
our target user and three observable acceptance criteria.”

## Session 2 — One complete workflow

Outcome: one browser action reaches the API and persists data in Supabase. The
student reviews every generated file and tests valid and invalid input.

Prompt: “Implement only this acceptance criterion. Preserve existing data and
secrets. Show the diff, explain the request path, and run the smallest relevant
checks.”

## Session 3 — Evidence-based debugging

Outcome: the student diagnoses one failure using the application response, GitHub
check, Vercel preview logs, or Supabase project state. They fix one responsible
layer and rerun the check.

Prompt: “Inspect this exact failure and rank likely causes. Do not reset data or
rewrite unrelated files. Fix the confirmed cause and demonstrate the original
failure is resolved.”

## Session 4 — GitHub to Vercel demonstration

Outcome: a reviewed pull request produces a working Vercel preview or production
deployment backed by the intended Supabase project. The student demonstrates the
workflow, persistence, limitation, and rollback path.

Checkpoint: the GitHub check passed, Vercel logs are understood, the service-role
key is server-only, and the previous deployment can be identified.
