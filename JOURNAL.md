# PathReview Development Journal

## Week 7 — Issue selection

**Issue link:** https://github.com/ascherj/pathreview/issues/153

**Issue title:** Faithfulness checker crashes when a context chunk has `text: None`

**Tier:** [ ] Tier 1  [X] Tier 2  [ ] Tier 3

**Problem summary:**
The faithfulness checker combines retrieved context into a single string before evaluating responses. If one of the context chunks contains a `text` field with the value `None`, the checker crashes because it attempts to join a non-string value. A successful fix will safely handle missing or `None` text values so the evaluation can continue without raising an error.

**Branch name:** `fix/153-faithfulness-none-context`

**Setup confirmation:** [x] App runs locally at localhost:5173

**Cohort ledger:** [X] Issue added to cohort ledger

### Is this issue right for me? 
Yes! I chose this issue because it is a manageable first open-source contribution that still requires real debugging and testing. Although the fix appears relatively small, I will need to understand how the faithfulness checker processes context and why the crash occurs before implementing a solution. This issue fits my current Python experience and will help me become more comfortable working in a larger codebase.

This issue has a clearly defined bug, a known failing test, and a limited scope, making it a good first open-source contribution. It requires debugging an existing codebase, understanding the cause of the crash, implementing a safe fix, and verifying it with automated tests. Since it is a Tier 1 issue, it is an appropriate starting point while still providing experience working with a larger project.

## Week 8 — Reproduction & solution planning

**Reproduction commit link:** [add after committing]

**Reproduction summary:**
I reproduced the issue by running the existing unit test `test_none_context_chunk_text` in `tests/unit/test_faithfulness_checker.py`. The test failed because the faithfulness checker attempted to join a `None` value with strings, confirming that context chunks with `text: None` cause a `TypeError`.

**PLAN.md link:** [add after pushing]

**Walkthrough video (recommended):** Not recorded

**Blockers or open questions:**
I still need to confirm whether the intended behavior is to skip chunks with `None` text or treat them as empty strings, although the issue description suggests safely converting them to empty strings.