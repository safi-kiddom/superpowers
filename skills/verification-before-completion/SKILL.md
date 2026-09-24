---
name: verification-before-completion
description: Use when about to claim work is complete, fixed, or passing, before committing or creating PRs - requires running verification commands and confirming output before making any success claims
---

# Verification Before Completion

## Overview

**Core principle:** A status claim is only as good as the evidence you ran for it in this session.

If you haven't run the command that proves a claim since your last change, you don't know that it holds. Say what you ran and what it showed; if you couldn't run it, say that instead of implying success.

## The Check

Before reporting that something works, is fixed, or is done:

1. **Identify** the command or observation that would prove the claim.
2. **Run** it fresh and in full, after your last change.
3. **Read** the output: exit code, failure count, warnings.
4. **Report** what it showed. If it contradicts the claim, report the actual state with the evidence.

## What Counts as Evidence

| Claim | Requires | Not sufficient |
|-------|----------|----------------|
| Tests pass | Test command output: 0 failures | Previous run, "should pass" |
| Linter clean | Linter output: 0 errors | Partial check, extrapolation |
| Build succeeds | Build command: exit 0 | Linter passing, logs look good |
| Bug fixed | Original symptom re-tested: passes | Code changed, assumed fixed |
| Regression test works | Red-green cycle verified | Test passes once |
| Agent completed | VCS diff shows the changes | Agent reports "success" |
| Requirements met | Each requirement checked against the result | Tests passing |

## Key Patterns

**Tests:**
```
✅ [Run test command] [See: 34/34 pass] "All tests pass"
❌ "Should pass now" / "Looks correct"
```

**Regression tests (TDD Red-Green):**
```
✅ Write → Run (pass) → Revert fix → Run (fails) → Restore → Run (pass)
❌ "I've written a regression test" (without red-green verification)
```

**Build:**
```
✅ [Run build] [See: exit 0] "Build passes"
❌ "Linter passed" (linter doesn't check compilation)
```

**Requirements:**
```
✅ Re-read plan → Check each item → Report gaps or completion
❌ "Tests pass, phase complete"
```

**Agent delegation:**
```
✅ Agent reports success → Check VCS diff → Verify changes → Report actual state
❌ Trust agent report
```

## When to Apply

Before any completion or success claim (including paraphrases like "that should do it"), and before committing, opening a PR, marking a task done, or moving to the next task.

This is about grounding claims in evidence you already have or can cheaply get, not about adding extra review passes. If the verification you ran while working already covers the claim and nothing changed since, cite it.
