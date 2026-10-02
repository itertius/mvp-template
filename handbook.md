# TA handbook

This handbook teaches beginners to direct an agentic IDE through a small MVP. The
template repository is documentation-only. The student’s application lives in a
separate GitHub repository and uses the reference delivery path GitHub → Vercel →
Supabase.

## Before class

- Read [skills.md](skills.md) and attach it to the agent if the IDE does not load
  repository instructions automatically.
- Confirm the student app repository, Supabase project, and Vercel project are
  separate and correctly named.
- Confirm the app repository has its own checks and keeps secrets out of GitHub.
- Connect Supabase MCP in read-only mode and Vercel MCP through OAuth. Use a
  least-privileged account and keep human confirmation enabled for mutations.
- Prepare a spare GitHub/Vercel/Supabase example using synthetic data.

## The teaching cycle

Use: **describe → plan → change → inspect → verify → explain**.

Use [the prompt framework](docs/prompt-framework.md) to turn each exercise into a
scoped request with observable acceptance and a safe handoff.

Ask the student to name the target user, problem, and one observable behavior.
Have the agent inspect the app repository before changing it. Review the complete
diff with the student. Test the success case, invalid input, and a failure state.
Ask the student to explain the browser request, API behavior, and Supabase data
change before moving to the next feature.

Use prompts with context, outcome, constraints, and acceptance criteria:

```text
Read the project instructions and inspect the existing application.
Context: [target user and current behavior]
Outcome: [one observable behavior]
Constraints: preserve existing data and keep the change small.
Acceptance: [success case and failure case]
Implement the smallest complete change. Explain the diff and report checks run.
```

## Four sessions

### 1. Scope and inspect

Students choose one audience, one problem, and one primary workflow. They inspect
the existing app with the agent and write three acceptance criteria.

Checkpoint: the student can explain which repository files own the UI, API, and
Supabase access. No implementation begins without a narrow acceptance condition.

### 2. Build one workflow

Students ask the agent to implement one complete browser-to-API-to-Supabase path.
They review the diff and test both valid and invalid input.

Checkpoint: another student can complete the workflow without agent or terminal
help, and the service-role key remains server-only.

### 3. Debug and prove

Students run the app repository’s checks, inspect Vercel preview logs, and diagnose
one controlled configuration or API failure. They verify that saved data remains in
Supabase after a new deployment.

Checkpoint: students distinguish an application bug, an environment-variable
problem, a Vercel deployment issue, and a Supabase schema issue using evidence.

### 4. Deploy and demonstrate

Students open a pull request, review the GitHub check, inspect the Vercel preview,
and promote only after acceptance checks pass. They demonstrate the live workflow,
known limitation, and rollback path.

Checkpoint: the live URL works for the intended audience, data is in the intended
Supabase project, and the student can identify the previous Vercel deployment.

## Safe operations

Never delete a Supabase project/table, rewrite production data, rotate a secret in
chat, or remove a Vercel deployment as a first troubleshooting step. Capture the
exact error and logs first. Use a preview project for schema experiments. Confirm
the Supabase project reference and Vercel project before any mutation.

Do not accept “the agent said it passed” as evidence. Require command output,
preview URL behavior, or a Supabase/Vercel observation that can be repeated.

## Assessment

Score each from 0–2: scope, agent collaboration, working workflow, verification,
and deployment. A score of 2 requires a student explanation and observable evidence.
Never collect credentials in submissions.
