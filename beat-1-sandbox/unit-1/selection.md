# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/48

**Verdict output**

**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

````
## Ranked read-out

**Accepted**

1. **#48: Add `Args:`/`Returns:`/`Raises:` docstring sections in `core/services/`.** This is the only accepted candidate.
   - **Fit:** It is contained, since it covers eight functions in two Python files, `profile_service.py` and `review_service.py`. It also means reading the code to document the different error paths. `delete_profile` re-raises after a rollback, while `process_review` marks the review failed and returns. That suits your interest in Python and backend logic, and you can verify it by tracing the behavior.
   - **Caveats:** The work is docs rather than tests or algorithms. The label is `tier-2` (Intermediate, 4–6 hours), not a newcomer label.
   - **Preferred checks:** `maintainer-engaged` passes because staff opened it. `newcomer-label` fails because it has no `good first issue`, `easy` or `help wanted` label.

**Rejected**

- **#64: Relevance scorer "partial overlap" test fixture.** It fails `unclear`-free on `unclaimed`. Open PRs #75, #87 and #232 already target the issue.
- **#57: Tech detector counts vendored and build-output files.** It fails `unclaimed` for the same reason. Open PRs #134, #174, #192 and a fork PR already target it.

**Note on the house rule:** `scope.md` says to ignore classmates' claim comments, and I did. That rule only changes part (3) of `unclaimed`. Part (2) still applies as written, so the open PRs sink #64 and #57. Both are good fits for your profile (Python, a test you can run, `good first issue`). The rubric rejects them anyway, and the fix belongs in the rubric, not in this run.

```json
[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/48",
    "checks": [
      {"name": "not-archived", "grade": "pass", "evidence": "archived: no; no archived banner, issues and PRs open"},
      {"name": "maintainer-alive", "grade": "pass", "evidence": "Newest main commit 2026-09-16 (40 days before 2026-10-26) by human account Aburke225"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "Last push to main 2026-09-16, within 180 days; no releases, which does not fail on its own"},
      {"name": "bounded-scope", "grade": "pass", "evidence": "One PR: add Args/Returns/Raises sections to eight public functions in two files; no umbrella, debate, core redesign, or support question; 0 comments"},
      {"name": "unclaimed", "grade": "pass", "evidence": "assignees: none; linked PRs: none; 0 comments, so no open PR or recent claim"},
      {"name": "ai-policy-allows", "grade": "pass", "evidence": "docs/CONTRIBUTING.md and the PR template have no AI statement; no AI_POLICY.md; silence passes"},
      {"name": "maintainer-engaged", "grade": "pass", "evidence": "Opened by Aburke225 (maintainer)"},
      {"name": "newcomer-label", "grade": "fail", "evidence": "Labels are docs and tier-2 (Intermediate); no good first issue, easy, or help wanted"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/64",
    "checks": [
      {"name": "not-archived", "grade": "pass", "evidence": "archived: no"},
      {"name": "maintainer-alive", "grade": "pass", "evidence": "Newest main commit 2026-09-16 by human account Aburke225, within 90 days"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "Last push to main 2026-09-16, within 180 days"},
      {"name": "bounded-scope", "grade": "pass", "evidence": "One fix: correct the test_query_with_partial_overlap fixture so overlap is genuinely partial; repro given"},
      {"name": "unclaimed", "grade": "fail", "evidence": "Assignees none, but open PRs #75, #87, #232 are linked to this issue; part (2) fails (the house rule only exempts classmates' claim comments in part (3))"},
      {"name": "ai-policy-allows", "grade": "pass", "evidence": "No AI statement in docs/CONTRIBUTING.md or the PR template; silence passes"},
      {"name": "maintainer-engaged", "grade": "pass", "evidence": "Opened by Aburke225 (maintainer)"},
      {"name": "newcomer-label", "grade": "pass", "evidence": "Labeled good first issue"}
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/57",
    "checks": [
      {"name": "not-archived", "grade": "pass", "evidence": "archived: no"},
      {"name": "maintainer-alive", "grade": "pass", "evidence": "Newest main commit 2026-09-16 by human account Aburke225, within 90 days"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "Last push to main 2026-09-16, within 180 days"},
      {"name": "bounded-scope", "grade": "pass", "evidence": "One fix: exclude node_modules/ and build/ paths in tech_detector.py; repro snippet and two named failing tests"},
      {"name": "unclaimed", "grade": "fail", "evidence": "Assignees none, but open PRs #134, #174, #192 and a fork PR target this issue; part (2) fails (the house rule only exempts claim comments in part (3))"},
      {"name": "ai-policy-allows", "grade": "pass", "evidence": "No AI statement in docs/CONTRIBUTING.md or the PR template; silence passes"},
      {"name": "maintainer-engaged", "grade": "pass", "evidence": "Opened by Aburke225 (maintainer)"},
      {"name": "newcomer-label", "grade": "pass", "evidence": "Labeled good first issue"}
    ],
    "verdict": "reject"
  }
]
```
````

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

Run 1 (full 20-issue run, saved as eval-run.txt): "agreement: 18/20 scored items  (bar: 18/20: PASS)".
Only one run occurred; it met the bar and the category floor on the first attempt, so the rubric was not revised.

**Issue analysis**

issue-20 (excalidraw/excalidraw): my rubric decided accept; the gold label is reject.
The run's note column reads "graded accept", and every required check passed. The repo is clearly alive ("2026-08-04 by dwelle"), there is no assignee or linked PR, and the policy line says "no statement on AI or contribution tooling". bounded-scope passed because the grader read the body as one feature: "Single toolbar shape feature; none of fail conditions (a)-(e) present".
The signal my rubric missed is who opened it: "opened by cursor[bot] (NONE); 0 comments, no maintainer in thread". An issue written by a bot that no human maintainer has confirmed is not a request the project has agreed it wants. My rubric only records that as the preferred check maintainer-engaged, which by design cannot change the verdict, so the issue slipped through.

**Check rationale**

Check: unclaimed. Pass condition as written: "All three hold: (1) assignees is `none`; (2) no OPEN pull request (linked, or mentioned in a comment, including PRs from forks) targets this issue; (3) no comment dated within 30 days of the capture date says the commenter is working on it or will take it, unless a later comment says that person stopped."
Why this form: a "good first issue" label says the issue is friendly, not that it is free, so the check looks at all three places a claim can live. It counts only OPEN PRs because closed, unmerged PRs are abandoned attempts, not active claims (those are handled by bounded-scope part (e)). It includes fork PRs and PRs mentioned only in comments because the evidence guide says to believe the thread when it disagrees with the sidebar. The 30-day window keeps an old, silent "I'll take this" from blocking an issue forever. The run caught all four claimed issues ("claimed 4/4").

**Trade-offs**

A case unclaimed accepts it will miss: a claim comment older than 30 days from someone still quietly working on it. Part (3) treats that claim as stale and lets the issue through, so a newcomer could end up duplicating work. I accept that, because a silent claim that old is more often abandoned, and the newcomer can ask in the thread before starting. The opposite trade-off also exists: any open PR blocks the issue, even a low-quality drive-by PR the maintainers will never merge.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

1. Fit: #48 asks for Args:/Returns:/Raises: sections on eight public functions in two Python files (core/services/profile_service.py and core/services/review_service.py). Python and backend logic are what I most want to work in, and the job is contained: one pull request, which the issue estimates at 4-6 hours. Each docstring has to match what the code actually does, so I have to trace the behavior myself, which is the kind of task I said I prefer.
2. The verdict correctly found that the repo is active (last commit 2026-09-16), the issue is unclaimed with no PRs or comments, and the scope is one PR. It also correctly rejected #64 and #57, which already have several open classmate PRs, even though both fit my profile better. What the rubric could not weigh is that #48 is documentation rather than a bug fix I can verify with a failing test, and that it is labelled tier-2 rather than good first issue. I accepted that trade because it is the only uncrowded option, and the issue spells out the behavior to document (delete_profile re-raises after a rollback; process_review marks the review failed and returns), so I can check every docstring against the code.
3. Claiming should be simple: nobody has commented or opened a PR, so I can be first. The harder part is accuracy: reading each function to see which arguments, return values and exceptions really apply, changing no behavior, and keeping CI (lint and typecheck) green on a docstring-only change.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
