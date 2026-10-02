# Prompt framework for agentic MVP work

Use this framework to turn a vague request into a small, verifiable agent task.
A good prompt gives the agent enough context to act without inventing product
scope, credentials, files, or success criteria.

## The seven blocks

1. **Role** — tell the agent whether it is planning, building, debugging, reviewing,
   or deploying.
2. **Context** — identify the repository, current behavior, target user, and
   relevant evidence. Ask it to inspect before editing.
3. **Outcome** — describe one user-visible result in a single sentence.
4. **Constraints** — name the stack, files or data to preserve, security rules,
   scope limits, and required compatibility.
5. **Acceptance** — define the success path, failure path, and observable proof.
6. **Process** — require a plan, focused diff, explanation, and checks. For risky
   operations, require confirmation before mutation.
7. **Handoff** — request changed files, commands run, results, limitations, and
   the next safe step.

## Base template

```text
Role: You are helping with [plan/build/debug/review/deploy].
Context: Inspect [repository/path]. The current behavior is [fact]. The target
user is [user] and the primary workflow is [workflow].
Outcome: Make [one observable result].
Constraints: Use [stack]. Preserve [data/API/files]. Keep scope to [boundary].
Never expose [secrets].
Acceptance: [success case]. [invalid or failure case]. Evidence must be [check,
URL, response, log, or screenshot].
Process: Inspect first. State a short plan. Make the smallest complete change.
Review the diff. Run focused checks. Do not perform destructive or production
mutations without my confirmation.
Handoff: Report files changed, checks and results, limitations, and the next step.
```

## Task modes

### Plan

```text
Inspect the repository and identify the smallest change that satisfies [criterion].
Do not edit files. List the owning files, risks, acceptance checks, and one
non-goal. Stop for clarification only if a missing fact changes the design.
```

### Build

```text
Implement only [criterion] in the existing application. Reuse its current seams.
Preserve the API and data described in [reference]. Add validation for [invalid
case]. Show the diff and run [check command].
```

### Debug

```text
The exact failure is: [command/URL/response/log]. Inspect before changing code.
Rank likely causes, test the cheapest safe hypothesis, and fix only the confirmed
cause. Do not reset data or rewrite unrelated files. Prove the original failure is
resolved and report what remains uncertain.
```

### Review

```text
Review this diff against [acceptance criteria]. Prioritize correctness, security,
data loss, and broken user workflows. For each finding give severity, file and
line, evidence, and a focused fix. If no finding exists, state what you verified
and what you could not verify.
```

### Deploy

```text
Inspect the authorized GitHub, Vercel, and Supabase project context first. Confirm
the target project and branch. Check the preview build, environment variables by
name (never print values), health endpoint, primary workflow, and persistence.
Require confirmation before production deployment, environment changes, domains,
schema changes, or data mutations. Report URLs, checks, and rollback target.
```

## MCP guardrails

MCP tools provide external context and actions; they do not replace application
code. Start Supabase MCP read-only. Use Vercel MCP to inspect previews and logs.
Never paste service-role keys, OAuth tokens, private keys, or full environment
files into a prompt. Confirm the project reference before querying or mutating.
Require human approval for production, schema, deployment, domain, environment,
or data changes.

## Prompt quality check

Before sending, ask: Is there one outcome? Can success be observed? Did I name what
must remain unchanged? Did I provide the current evidence? Is the requested action
reversible? Does the agent know when to stop? If any answer is no, tighten the
prompt before asking for implementation.

## Thai classroom example

ใช้ตัวอย่างนี้เป็น prompt เริ่มต้นสำหรับนักเรียนที่ต้องการสร้าง MVP จัดการงานที่
ต้องส่ง การกำหนดขอบเขตให้เหลือหลักสำคัญหนึ่งอย่างช่วยให้ agent สร้างงานที่เสร็จ
และทดสอบได้ภายในเวลาเรียน

```text
[Role]
คุณคือนักพัฒนาเว็บแอปที่ช่วยสร้าง MVP ให้นักเรียนมัธยมเสร็จภายใน 60 นาที

[ปัญหาและผู้ใช้]
ผู้ใช้คือนักเรียน ม.4 ที่มีกิจกรรมหลังเลิกเรียน ครูส่งงานหลายช่องทาง เช่น LINE,
Classroom และ Messenger ทำให้นักเรียนพลาดงานหรือกำหนดส่ง เราอยากรวบรวมงานทุกวิชา
ไว้ในที่เดียว

[หลักสำคัญ 1 อย่าง]
รวบรวมงานที่มีวันส่งไว้ในรายการเดียว และเรียงตามวันที่ใกล้ที่สุด

[User flow 3 ขั้น]
1. กดปุ่ม “+ เพิ่มงาน” แล้วกรอกชื่องาน วิชา และวันส่ง
2. หน้าหลักแสดงงานทั้งหมด เรียงตามวันที่ใกล้ที่สุด และแยกงานที่ใกล้ถึงกำหนด
3. เมื่องานเสร็จ ผู้ใช้กดติ๊ก งานจะย้ายไปส่วน “ส่งแล้ว” ด้านล่าง

[หน้าจอ 1–2 หน้า]
- หน้าหลัก: รายการงานและปุ่มเพิ่มงาน
- ฟอร์มเพิ่มงาน: เปิดเป็นหน้าใหม่หรือ popup ก็ได้

[ข้อจำกัด]
- ทำเฉพาะ flow หลักนี้ก่อน
- ใช้ข้อมูลจำลองได้ถ้ายังไม่ได้เชื่อมฐานข้อมูล
- อย่าเพิ่ม login, notification หรือฟีเจอร์อื่นก่อน

[ก่อนเริ่ม]
สรุปแผนที่จะสร้างเป็นข้อ ๆ พร้อมรายชื่อไฟล์ที่จะเปลี่ยนและวิธีตรวจสอบให้ดูก่อน
ห้ามเริ่มเขียนโค้ดจนกว่าฉันจะตรวจแผนและตอบว่า “เริ่มได้”
```

หลังจากนักเรียนอนุมัติแผน ให้ส่ง prompt ต่อว่า:

```text
เริ่มได้ ทำตามแผนที่อนุมัติไว้ทีละขั้น เปลี่ยนเฉพาะไฟล์ที่จำเป็น
หลังแต่ละขั้นให้สรุป diff และบอกวิธีทดสอบ flow สำเร็จและกรณีข้อมูลไม่ครบ
```
