# CCAR-F Practice Questions – Answers & Explanations

Each answer gives the correct letter, why it is right, and why the most tempting wrong option fails.

## Domain 1 answers (Q1–Q28)

**Q1 — B.** `stop_reason` is the API's structured signal: `tool_use` means run tools and continue, `end_turn` means done. Checking the text for a magic token (A) is the same fragile natural-language parsing that caused the bug.

**Q2 — A.** Every `tool_result` must answer a `tool_use` block in the immediately preceding assistant turn, so that turn has to be sent back unchanged. Starting new conversations (C) loses all context.

**Q3 — C.** Results for parallel tool calls go back together in one user message, each matched by its own `tool_use_id`. Separate user messages (A) break the expected pairing and the parallel-tool pattern.

**Q4 — A.** An error result with `is_error: true` keeps the loop alive and lets Claude decide to retry, try another tool, or tell the user. An empty result (B) hides the failure and leads Claude to conclude there is no order.

**Q5 — D.** A rule that must hold every time belongs in code: a hook or gate is deterministic. Prompt wording (A), examples (B) and temperature (C) only lower the failure rate; they cannot remove it.

**Q6 — B.** A subagent starts with only the prompt it is given; it never sees the coordinator's history. Model size (A) is irrelevant when the subagent does not even know the topic.

**Q7 — A.** Dynamic selection runs only the subagents a query needs. One subagent with every tool (B) loses specialization and makes tool choice worse.

**Q8 — B.** Subagents are spawned through the Task (Agent) tool, so the coordinator must be allowed to call it. Without it the subagent definitions exist but can never be invoked; description length (A) affects choice, not availability.

**Q9 — C.** Several Task calls in one response let the subagents run at the same time. The Batch API (D) has no latency guarantee, so it is the opposite of "as fast as possible".

**Q10 — D.** Least privilege means only the tools the role needs. A prompt telling it not to write (C) is a probabilistic guard on a capability it should never have had.

## Domain 2 answers (Q29–Q49)

**Q29 — B.** Team rules belong in the project `CLAUDE.md`, which is committed and loaded for everyone. `CLAUDE.local.md` (C) is personal and gitignored, so it has the same problem as the user file.

**Q30 — C.** A personal preference for one project goes in an uncommitted, personal memory file. The project `CLAUDE.md` (A) would push the preference onto the whole team.

**Q31 — A.** Imports and rules files keep memory modular and maintainable without losing content. Moving it to user files (C) removes it from the shared repo and from new teammates.

**Q32 — D.** Path-scoped rules load only when Claude works on matching files, wherever they live. A `CLAUDE.md` in every test folder (A) duplicates the rules and drifts out of sync.

**Q33 — B.** A project slash command in `.claude/commands/` is shared through git and started with `/release-prep`. A personal command (C) only exists on one machine.

**Q34 — C.** `context: fork` runs the skill in an isolated subagent context and returns only the result. `allowed-tools` (A) limits tools but does nothing about clutter.

**Q35 — A.** `allowed-tools` restricts which tools Claude may use while the skill is active. `context: fork` (B) isolates context but does not restrict tools.

**Q36 — D.** Claude decides to use a skill by matching the task against its `description`, so it must say what the skill does and when to use it. Folder location (A) affects who has the skill, not whether it is chosen.

**Q37 — B.** Skills use progressive disclosure: only the name and description are in context until the skill is needed. Putting everything in `CLAUDE.md` (A) spends context on every session.

**Q38 — C.** Plan mode is meant for large, multi-file or unclear changes: you review the approach before any file is touched. Editing freely and reverting (D) wastes effort and risks half-done changes.

## Domain 3 answers (Q50–Q70)

**Q50 — B.** Explicit include/exclude criteria tell Claude exactly what counts as an issue. Vague confidence wording (A) is what is already failing.

**Q51 — A.** Defined levels with examples give a stable rubric, so the same issue gets the same rating. Averaging two inconsistent answers (B) does not fix the missing definition.

**Q52 — C.** Removing or tightening the noisy category restores trust while keeping the valuable findings. Turning the whole bot off (A) throws away the categories that work.

**Q53 — A.** A nullable field gives Claude a valid way to say "not present", and the example shows it in action. Making the field required (C) actually pushes Claude to invent a value.

**Q54 — B.** Diverse examples teach the underlying rule rather than one surface format. More of the same layout (A) deepens the overfitting.

**Q55 — C.** A forced tool call with a schema (or structured outputs) guarantees parseable JSON. A prompt instruction (A) and regex cleanup (B) still fail some of the time.

**Q56 — D.** Schemas enforce syntax and types, not meaning, so business rules must be checked in code. Nothing is wrong with the schema (A); it is doing its job.

**Q57 — B.** `any` forces a tool call but lets Claude pick which tool. A named tool (C) would always force the invoice tool, even for receipts.

**Q58 — A.** An escape-hatch value plus a detail field lets Claude say "none of these" honestly. Adding endless categories (C) never covers every real document.

**Q59 — C.** Feeding the specific validation error back tells Claude exactly what to re-check. Retrying the identical prompt (A) tends to produce the same mistake.

## Domain 4 answers (Q71–Q89)

**Q71 — A.** Tool descriptions are Claude's main signal for choosing a tool, so overlapping descriptions cause wrong choices. A system-prompt patch (B) treats the symptom and leaves the overlap in place.

**Q72 — B.** A sweeping system-prompt instruction can override good tool descriptions. Reword it so it says when the knowledge-base search applies. Lengthening descriptions (A) does not remove the conflicting instruction.

**Q73 — C.** Fewer, relevant tools per agent make selection more accurate. More prompt detail (A) adds context but keeps 18 options to choose from.

**Q74 — A.** A higher-level tool that matches the task removes the error-prone chaining. More ordering instructions (B) still rely on Claude getting four calls right every time.

**Q75 — D.** Tool results should carry the meaningful, relevant information Claude needs to reason. A longer description (A) does not fix a noisy result.

**Q76 — A.** "Could not check" and "checked, found nothing" must look different, or the agent draws false conclusions. A prompt hint (B) asks Claude to guess which case it is.

**Q77 — C.** A category and a retryable flag let the agent retry temporary failures and stop on permanent ones. A global retry limit (A) also stops useful retries of temporary errors.

**Q78 — D.** Temporary errors are best retried close to where they happen; only failures that persist go up, with context. An empty "success" (B) hides the gap from the final report.

**Q79 — D.** Forcing the named tool guarantees it is called. A system-prompt instruction (B) is probabilistic.

**Q80 — C.** Least privilege: each role gets only the tools it needs. Telling the subagent not to use payment tools (A) leaves a dangerous capability one mistake away.

## Domain 5 answers (Q90–Q105)

**Q90 — A.** Summaries lose exact values; a persistent facts block keeps them intact on every turn. Summarizing more often (B) loses even more detail.

**Q91 — B.** Trimming before results enter context keeps only what matters, deterministically. Telling Claude to ignore fields (A) still spends the tokens and dilutes attention.

**Q92 — D.** Models attend best to the start and end of long contexts ("lost in the middle"). Repeating the instruction in the middle (A) keeps it in the weakest spot and adds noise.

**Q93 — C.** The cache matches an exact prefix, so anything that changes must come after the cached part. Disabling caching (A) throws away large savings.

**Q94 — B.** An explicit request for a human should be honoured at once, with a structured handoff. Trying to resolve it first (A) ignores what the customer asked for.

**Q95 — D.** Model self-confidence does not track real accuracy well, so it makes a poor sole trigger. Changing the threshold (A) does not fix an unreliable signal.

**Q96 — C.** When policy does not cover a case, the agent should not invent policy; a human decides. Using its own judgment (A) means the agent is making policy.

**Q97 — B.** With several matches, ask for a unique identifier rather than guess. Picking one (A, C) risks acting on the wrong person's account.

**Q98 — D.** Partial results with a clearly marked gap are more useful than nothing and are honest. Leaving the section out silently (B) misleads the reader.

**Q99 — A.** Reporting failure as success hides it from every later step. Crashing the whole system (C) is the opposite extreme; the right answer is to report the failure with context.

**Q11 — D.** The agent should break the message into its separate concerns and close each one. Pushing the work onto customers (A) or humans (B) avoids fixing the agent.

**Q12 — C.** A human cannot read the agent's context, so the handoff must carry the key facts in a fixed structure. A raw transcript (A) technically holds the facts but forces the human to dig through it.

**Q13 — A.** `PostToolUse` runs on every tool result, so normalizing there fixes the data deterministically at the source. A system-prompt note (B) still relies on Claude converting correctly every time.

**Q14 — D.** `PreToolUse` runs before the call, so it can stop the refund from ever happening. Reversing afterwards (A) or checking at the end (C) means the non-compliant refund was already issued.

**Q15 — B.** The steps are known in advance, so a fixed chain fits: focused per-file passes plus a pass for cross-file issues. "Be thorough" (A) does not fix the attention dilution of one giant pass.

**Q16 — C.** The cause is unknown, so the plan must adapt to findings. A fixed chain (A) assumes you already know the steps.

**Q17 — B.** The earlier tool results are stale. Either tell the resumed session what changed or restart with a summary. `fork_session` (D) branches a session; it does not refresh old results.

**Q18 — D.** Forking creates independent branches from one shared baseline. Brand-new sessions (C) would have to redo the analysis and could diverge from the baseline.

**Q19 — A.** Routing classifies the input and sends it to a specialized prompt or tool set. Voting (C) runs the same task several times to compare answers; it does not specialize.

**Q20 — C.** Clear criteria plus measurable improvement from feedback is the textbook case for evaluator–optimizer. Chaining with no checks (B) never catches the missed rules.

**Q21 — B.** `max_tokens` means the output was cut off, not finished. Treating it as `end_turn` (A) silently returns a truncated report.

**Q22 — C.** `pause_turn` means a long server-tool turn was paused; sending the response back lets Claude carry on. It is not an error (A).

**Q23 — D.** `stop_reason` is the real completion signal; a cap is only there to stop runaway loops. Saying the cap is the recommended stop condition (A) is the classic distractor.

**Q24 — A.** Start with the simplest design that works; multi-agent systems cost many more tokens and add coordination overhead. "Always more accurate" (B) is an absolute claim and wrong.

**Q25 — A.** Subagents exist partly to keep the coordinator's context clean, so they should return distilled results. A larger window (B) postpones the problem and still buries key facts in noise.

**Q26 — C.** In hub-and-spoke designs all communication flows through the coordinator, which keeps control and traceability. Direct messaging (A) or shared mutable state (B) breaks that model.

**Q27 — B.** Iterative refinement: the coordinator checks coverage and sends targeted follow-ups. Delivering a known gap (A) or inventing numbers (D) gives the user an incomplete or misleading answer.

**Q28 — D.** Claude reads the `description` to decide when a subagent fits the task, so write it as "use this when…". `prompt` (C) is the subagent's own system prompt, used after it is chosen.

**Q39 — A.** A small, well-defined change needs no plan; direct execution is fastest. Plan mode (B) adds overhead with no benefit here.

**Q40 — C.** The Explore subagent keeps its search output in its own context and hands back a summary. `/compact` (B) only shrinks context after it has already filled.

**Q41 — B.** Concrete examples and tests remove ambiguity that prose cannot, and tests give a clear pass/fail target. More prose (A) repeats what has already failed.

**Q42 — A.** The interview pattern makes Claude surface the questions and edge cases before writing code. Plan mode (C) explores code; it does not talk to stakeholders.

**Q43 — D.** `-p` runs headless, `--output-format json` gives parseable output, and `--json-schema` fixes its structure. Driving interactive mode with scripts (A) is fragile.

**Q44 — D.** A session that wrote the code is biased toward its own reasoning; an independent session reviews it fresh. "Be very critical" (A) is a prompt tweak on a structural problem.

**Q45 — C.** Giving the reviewer the earlier findings lets it report only new or unresolved issues. Reviewing only the first push (A) misses problems added later.

**Q46 — A.** `--allowedTools` limits what the job may run and `--max-turns` caps how long it runs. `--verbose` (B) only adds logging.

**Q47 — B.** A deny rule in the committed project settings is enforced for everyone. A `CLAUDE.md` line (C) is guidance Claude might not follow; local settings (D) apply only to one developer.

**Q48 — D.** A hook runs every time the matching tool runs, so formatting is guaranteed. A `CLAUDE.md` instruction (A) is probabilistic.

**Q49 — C.** Permission rules check deny first, then ask, then allow, and rules from all settings files combine. Saying project overrides user (A) confuses precedence for single values with how permission rules are evaluated.

**Q60 — D.** Retries only help when the information exists and Claude misread it. When it is missing, return `null` and send the document to a human; estimating (C) fabricates data.

**Q61 — B.** Keeping both values plus a flag makes conflicts explicit and easy to query. Storing only the stated total (A) hides every mismatch.

**Q62 — A.** Large, non-urgent, cost-sensitive work is what batches are for: 50% cheaper, results within 24 hours. A synchronous loop (B) costs double and hits rate limits.

**Q63 — D.** A blocking check needs a predictable response time, and batches promise none. Option C is false: batch requests can include tool definitions; what they lack is a multi-turn loop.

**Q64 — A.** Batch results are not guaranteed to come back in input order; `custom_id` is how you match them. Timestamps (B) do not identify which input a result belongs to.

**Q65 — B.** A batch request is a single Messages API call. Running tool calls, sending results back and calling again is orchestration you must build yourself.

**Q66 — C.** For long inputs, put the document first and the question at the end; this measurably improves answers. Putting the question first (A) is the weaker ordering.

**Q67 — A.** Claude follows rules better when it knows the reason, and generalizes the reason to similar cases. Capitals and repetition (B, C) are weaker signals.

**Q68 — D.** Reasoning before answering (or extended thinking) improves accuracy on multi-step problems. Asking for the answer only (A) removes that space to reason.

**Q69 — C.** An independent checker is not anchored on the first extraction's reasoning. Asking the same conversation to re-check (A, B) tends to confirm its earlier answer.

**Q70 — D.** Tags plus an explicit statement separate trusted instructions from untrusted data. Putting untrusted email text in the system prompt (A) gives it more authority, not less.

**Q81 — A.** Project scope (`.mcp.json` in the repo) is how a team shares MCP servers through git. Per-user configs (B) drift and leave new teammates without the server.

**Q82 — B.** `.mcp.json` supports environment-variable expansion, so the file is shared and the secret is not. Committing the token (A) leaks it to everyone with repository access, now and in history.

**Q83 — B.** User scope is personal and applies across all your projects. Project scope or a committed `.mcp.json` (A, C) would share it with the team.

**Q84 — C.** Resources are application-controlled, read-only data exposed as context, such as a schema catalog. Tools (A) are actions the model decides to call.

**Q85 — B.** Remote MCP servers use the Streamable HTTP transport; stdio (A) is for local processes. The older SSE transport (C) is deprecated, not recommended.

**Q86 — D.** A maintained existing server saves build and upkeep effort; build your own only for real gaps. Building your own by default (A) adds cost for no gain.

**Q87 — B.** Glob matches file names and paths by pattern. Grep (A) searches file contents, not names.

**Q88 — C.** Grep searches file contents by regex, which is exactly a call-site search. Glob (A) only matches file names.

**Q89 — D.** Edit needs a unique `old_string`; add context until it is unique, or Read and Write the whole file for a big rewrite. A global `sed` (C) changes all 12 occurrences, not just the one you meant.

**Q100 — C.** Notes on disk survive compaction and new sessions, and subagents keep raw search output out of the main context. A larger model (D) only delays the same problem.

**Q101 — A.** A progress manifest makes long work resumable after a crash or context reset. Relying on Claude's memory (B) fails exactly when the session is lost.

**Q102 — B.** Stratified sampling measures accuracy for each type and field, so weak segments show up. A random overall sample (A) is dominated by the easy majority.

**Q103 — D.** Calibrated field-level scores target human effort where errors are likely, and ongoing sampling catches drift. A single document-level score (A) hides which field is wrong.

**Q104 — A.** Provenance has to be captured when a fact is found and carried through to the final claim. A bibliography (B) lists sources but does not say which claim came from which source.

**Q105 — C.** Report conflicting data openly with sources and dates; let the reader see the disagreement. Averaging (B) invents a number that neither source supports.
