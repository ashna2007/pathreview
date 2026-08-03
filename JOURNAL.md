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

**Reproduction commit link:** https://github.com/ascherj/pathreview/commit/06f132bf497e1620de48d64fe8d0edd282257369 

**Reproduction summary:**
I reproduced the issue by running the existing unit test `test_none_context_chunk_text` in `tests/unit/test_faithfulness_checker.py`. The test failed because the faithfulness checker attempted to join a `None` value with strings, confirming that context chunks with `text: None` cause a `TypeError`.

**PLAN.md link:** https://github.com/ashna2007/pathreview/blob/fix/153-faithfulness-none-context/PLAN.md

**Walkthrough video (recommended):** Not recorded

**Blockers or open questions:**
I still need to confirm whether the intended behavior is to skip chunks with `None` text or treat them as empty strings, although the issue description suggests safely converting them to empty strings.

## Week 9 — Solution building & PR submission

### Check-in 1 (mid-week)

**Current progress:**
Implemented the fix for Issue #153 by updating the faithfulness checker to safely handle context chunks whose `"text"` field is `None`. I verified that the previously failing test now passes, and the full unit test results improved from 53 failures and 375 passes to 52 failures and 376 passes.

**Next steps:**
Push my branch, open a draft pull request, complete the PR template, request peer or mentor feedback, address any feedback I receive, and finalize the pull request.

**Blockers:**
None.

### Check-in 2 (end of week)

**PR link:** https://github.com/ascherj/pathreview/pull/665

**Branch:** `fix/153-faithfulness-none-context`

**What you built:**
Implemented a fix for Issue #153 by updating the faithfulness checker to safely handle context chunks whose `"text"` field is `None`. This prevents a `TypeError` during context concatenation while preserving the existing behavior for valid text.

**Tests added or updated:**
No new tests were added. The existing unit test `test_none_context_chunk_text` now passes after the fix. I also verified that `make test-unit` improved from 53 failed / 375 passed to 52 failed / 376 passed.

**Self-review confirmation:**
- [x] `make check` introduces no new failures (182 pre-existing errors remain)
- [x] `make test-unit` introduces no new failures (improved from 53 failed to 52 failed)

**Draft PR feedback received from:**
none