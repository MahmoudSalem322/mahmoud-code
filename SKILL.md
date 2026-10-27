---
name: mahmoud-code
description: Mahmoud's workflow for building projects and large features. First builds a research-backed plan, splits it into detailed numbered tasks, and recommends the execution approach, model and effort for each task. Then, each time the user writes "task N", it executes that task with Superpowers, runs a full code review and tests, runs security testing, and writes a detailed report. Use ONLY when the user explicitly asks for this skill by name, for example "use mahmoud-code" or "استخدم سكيل mahmoud-code". Never start it on your own for any other request.
---

# mahmoud-code

A five-stage workflow. Stage 1 runs once for the project or feature. Stages 2 to 5 run for each task, in order, when the user names the task.

## When to plan

The plan (Stage 1) is for large work: a new project, a big feature, a change that spans many parts. When the user asks for a small detail, use your own judgment on how to handle it.

## Subagents

Use subagents as needed, at any stage. Before starting them, tell the user which subagents you want to use and for what, then wait for the user's approval. Do not start any subagent without it. This includes subagents that other skills start, such as Superpowers' `subagent-driven-development`.

## Suggestions and external sources

During execution, give professional suggestions when they would help, for example a specific MCP server or a source from a website. Before connecting to any MCP server or using a source from any website, tell the user what it is and why you want it, then wait for the user's approval.

## Tone in code review and the report

In the code review (Stage 3) and the report (Stage 5), speak like a professor of software engineering: expert, precise and very professional. Keep it clear enough for the user to fully understand: explain technical terms and the reasoning behind each finding.

## Stage 1: Plan, then tasks

1. **Plan.** Build a plan for what the user wants to do. Base it on deep analysis: use your research abilities (web search, documentation, the existing code) and think it through before writing it.
2. **Tasks.** From the plan, write clear, numbered tasks. Each task is detailed and contains:
   - What the task includes.
   - What will be changed in it.
   - The expected outputs.
3. **Execution recommendation.** For each task, recommend in detail:
   - How to execute it.
   - The suitable model.
   - The suitable effort level.
4. **Wait.** Stop and wait for the user to write a task number (`task 1`, `task 2`, ...). Each task is executed by its number.

## Stage 2: Execute the task

Starts when the user writes `task N`. Execute task N using the Superpowers skills:

- `executing-plans` or `subagent-driven-development`
- `test-driven-development`

## Stage 3: Code review and testing

Starts automatically when Stage 2 ends. Together with Superpowers:

- A full code review of the task: `requesting-code-review`, then `receiving-code-review` to act on the findings.
- A test for every part of the task.
- `verification-before-completion` before moving on.

## Stage 4: Security testing

Starts when Stage 3 ends. Use these security skills:

- `owasp-security` (from `agamm/claude-code-owasp`): review against OWASP Top 10:2025, ASVS 5.0, and OWASP for LLM and agentic applications.
- `static-analysis` (from `trailofbits/skills`): automated scanning with Semgrep and CodeQL.
- `/security-review`: built into Claude Code (Claude Code only).

Together with Superpowers: `systematic-debugging` to fix the vulnerabilities found, and `verification-before-completion` to confirm the fixes.

If one of these skills is not available in the current agent, say so in the report and continue with the others.

## Stage 5: Detailed report

A fully organized report, in this order:

1. **Task name.**
2. **Outputs:** what was produced.
3. **Modified files (very important):** in detail, as bullet points. For each file:
   - What changed in it.
   - Whether best practices were used.
4. **Stage results:** a section for the results of Stage 2, Stage 3 and Stage 4, including the results of every test.
5. **Risks:** remaining risks, the security testing results, and proposed solutions.
6. **Final results:** confirmation that the task is implemented 100% correctly, and an evaluation of everything done in it.
