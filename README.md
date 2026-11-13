# Claude Certified Architect – Foundations (CCAR-F) Study Guide

Study notes, worked examples and 105 practice questions for Anthropic's **Claude Certified Architect – Foundations** exam (CCAR-F, formerly CCA-F).

> **Unofficial.** These notes are not affiliated with or endorsed by Anthropic. The official exam guide is not public. The domain list, weights and scenario names come from public third-party prep material. They are checked against Anthropic's documentation where possible. Verify anything critical against the [Claude docs](https://docs.claude.com) and the [Claude Code docs](https://code.claude.com/docs).

## Exam at a glance

| | |
| --- | --- |
| Questions | 60 multiple choice, scenario-based |
| Time | 120 minutes |
| Passing score | 720 / 1000 (scaled) |
| Scenarios | 4 of the 6 scenarios below are picked at random for each candidate |
| Guessing | No penalty for wrong answers, so answer every question |

| # | Domain | Weight | ≈ Questions |
| --- | --- | --- | --- |
| 1 | Agentic Architecture & Orchestration | 27% | 16 |
| 2 | Claude Code Configuration & Workflows | 20% | 12 |
| 3 | Prompt Engineering & Structured Output | 20% | 12 |
| 4 | Tool Design & MCP Integration | 18% | 11 |
| 5 | Context Management & Reliability | 15% | 9 |

## Contents

| File | What it covers |
| --- | --- |
| [00-Study-Notes.md](00-Study-Notes.md) | Condensed revision notes for the day before the exam: all five domains, the six scenarios and a last-day checklist |
| [01-Domain1-Agentic-Architecture-and-Orchestration.md](01-Domain1-Agentic-Architecture-and-Orchestration.md) | The agentic loop and `stop_reason`, workflow patterns, coordinator–subagent design, Agent SDK subagents and hooks, enforcement in code, sessions (resume / fork) |
| [02-Domain2-Claude-Code-Configuration-and-Workflows.md](02-Domain2-Claude-Code-Configuration-and-Workflows.md) | CLAUDE.md hierarchy, `.claude/rules` with `paths:`, slash commands, skills, subagents, settings precedence, plan mode, CI/CD with `claude -p` |
| [03-Domain3-Prompt-Engineering-and-Structured-Output.md](03-Domain3-Prompt-Engineering-and-Structured-Output.md) | Explicit criteria, few-shot examples, `tool_choice`, JSON schemas, validate-and-retry loops, Message Batches API |
| [04-Domain4-Tool-Design-and-MCP-Integration.md](04-Domain4-Tool-Design-and-MCP-Integration.md) | Tool descriptions, structured errors, MCP primitives, transports and scopes, Claude Code built-in tools |
| [05-Domain5-Context-Management-and-Reliability.md](05-Domain5-Context-Management-and-Reliability.md) | Long-context strategy, case-facts blocks, prompt caching, escalation criteria, error propagation, sampling and provenance |
| [06-Exam-Scenarios.md](06-Exam-Scenarios.md) | The six scenarios, each with a reference architecture, common failures, fixes and two worked questions |
| [07-Practice-Questions.md](07-Practice-Questions.md) | 105 scenario-style practice questions, split by domain weight |
| [08-Practice-Answers-and-Explanations.md](08-Practice-Answers-and-Explanations.md) | Answer key: why each right answer is right and why the most tempting wrong option fails |

Each domain file has the same structure: concepts → Python examples → an **Exam traps** list after each section → a summary trap table → key facts to memorize.

## The six scenarios

1. Customer Support Resolution Agent
2. Code Generation with Claude Code
3. Multi-Agent Research System
4. Developer Productivity with Claude
5. Claude Code for CI/CD
6. Structured Data Extraction

## Suggested study plan

1. **Learn:** read the five domain files in order of weight (1 → 2 → 3 → 4 → 5). Stop after each section to go over its exam traps.
2. **Apply:** read [06-Exam-Scenarios.md](06-Exam-Scenarios.md) and answer the worked questions before you read the answers.
3. **Test:** answer all 105 questions in [07-Practice-Questions.md](07-Practice-Questions.md) on paper, then mark them against [08-Practice-Answers-and-Explanations.md](08-Practice-Answers-and-Explanations.md). Aim for at least 75%, which leaves a margin over the ~72% pass mark. Re-read the domain file for any question you miss.
4. **Revise:** read [00-Study-Notes.md](00-Study-Notes.md) the day before the exam.

When two answers both look plausible, pick the one that is **deterministic** (code, hooks, schemas) over the one that only *asks* the model nicely. Pick the one that is **explicit** (state the criteria, pass the context) over one that relies on inference. Pick the **simplest** design that meets the requirement.

## Notes and caveats

- **Code examples** are in Python, using the `anthropic` SDK and `claude_agent_sdk`. They are study examples and were not executed as tests.
- **Forced `tool_choice`:** the exam treats forcing a tool (`tool_choice: {"type": "tool", ...}` or `"any"`) as the way to guarantee structured output. On the newest models (Claude Opus 5.5, Sonnet 5.5, Fable 5.1+), forced `any` / `tool` returns a 400 error. There you use `tool_choice: auto` with `strict: true`, or structured outputs (`output_config.format`). On the exam, still choose the forced-tool answer.
- **Task vs Agent tool:** Claude Code renamed the subagent tool from **Task** to **Agent**, so exam wording may use either name.
- **Not checked against official docs (Domain 2):**
  - the output field returned with `--json-schema`
  - managed-policy CLAUDE.md file locations
  - `claude-code-action` inputs
- **Diagrams** are in [Mermaid](https://mermaid.js.org/), which GitHub renders natively.

## License

Personal study material. Add a license (for example [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)) before you share or reuse it publicly.
