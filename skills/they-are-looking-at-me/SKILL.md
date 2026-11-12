---
name: they-are-looking-at-me
description: Restore a broken app, failing demo, or interrupted workflow under immediate time pressure with a small, reversible fix and direct verification. Use when the user says "they are looking at me", "please just make it work", or asks for urgent recovery. Not for routine feature development or a full incident postmortem.
---

# They Are Looking at Me

> please fix it, they are looking at me right now.

Get the user's critical path working again. Optimize for time to a verified recovery, keep the change small, and save the architectural discussion for later.

## Find the path that matters

Infer the immediate success condition from the conversation and available environment: the app starts, the demo button works, the build passes, or the affected request completes. If the target is genuinely ambiguous, ask one short question while inspecting what is available. Do not start with a questionnaire or a long plan.

Briefly state what you are restoring, then inspect the failure and the nearest useful evidence: the exact error, relevant logs, recent diff, process state, or configuration. Read local project instructions. Preserve uncommitted work. Avoid a repository-wide investigation unless the evidence leads there.

If the deadline is known, choose a remedy that can be applied **and checked** before it. Do not spend the entire window diagnosing a perfect fix.

## Restore first

Choose the fastest evidence-supported intervention with a small blast radius. Depending on the failure, this may be reverting a specific regression, correcting a configuration value, restoring a compatible dependency, fixing a narrow code path, or disabling a broken optional feature through an existing flag. Prefer a known-good rollback over an uncertain rewrite when rollback is compatible with current data and schema.

Before changing state, know how to undo your change. Apply the remedy within the user's existing authorization; do not repeatedly ask for permission already given. Urgency does not authorize a new production deployment, destructive data operation, or external action outside that scope. When access or authorization is missing, finish the concrete local fix and checks, then request only the missing action or access.

Keep the intervention proportional:

- No unrelated cleanup, framework migration, dependency-wide upgrade, or speculative refactor.
- Never bypass authentication, authorization, payment integrity, or data validation to make a screen turn green.
- Do not swallow failures, fabricate successful responses, or replace real production data with mock data. A demo-only fallback is acceptable when the user has authorized it and it is clearly identified as such.
- Degraded operation must remain honest: preserve the core path and make unavailable functionality visible.
- Do not reset the working tree or revert somebody else's unrelated changes. Check data and migration compatibility before rolling back an application version.

If an attempt fails, use the new evidence before trying again. Do not stack speculative patches or repeat a failed restart unchanged. Undo your ineffective changes where safe, preserving unrelated work. If the same hypothesis fails twice without new evidence, switch hypotheses or report the concrete blocker. Never loop on retries that can duplicate writes, charges, or jobs.

## Prove that it works

Run the smallest check that exercises the original failure and the user's success condition. A successful compile alone does not prove that a broken interaction or production request is restored. For a UI failure, exercise the affected interaction when possible. For a service failure, check the affected request and its meaningful result. Avoid replaying real transactions; use a safe test path.

Run relevant required project checks. When time or access prevents broader verification, say exactly what remains unchecked. Keep local validation, deployment, and observed production recovery distinct. Do not call the incident resolved merely because a patch exists.

If the critical path works, stop expanding the patch. Leave a brief, actionable follow-up for temporary compromises. If recovery is blocked, report what failed and the single next action needed; do not imply success.

## Hand back control

Keep progress updates calm, short, and practical. No blame, lectures, or panic theater. End with a compact report adapted to the situation:

```text
Status: Working / Degraded / Blocked (state the environment).
Changed: What restored the critical path.
Verified: The actual check and observed result.
Undo: The precise way to reverse this change.
Later: Any temporary compromise and the next repair, if needed.
```

Use actual evidence and commands or file references when available. Never invent a verification result. The meme is the entry point; a working, honestly verified system is the deliverable.
