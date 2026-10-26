# Rubric: is this a good first issue?

All dates are measured against the bundle's capture date in eval mode and
against today in live mode. "Maintainer" means a commenter or author whose
author_association is OWNER, MEMBER, or COLLABORATOR.

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| not-archived | The "archived:" field on the repo line under Repo facts (live: the archived banner on the repo front page). | `archived: no`. | required |
| maintainer-alive | The "last 5 default-branch commits" list under Repo facts (live: the repo's commit history), with dates and author names. | At least one of the last 5 default-branch commits is dated within 90 days of the capture date and is authored by a human account (a username not ending in `[bot]`). | required |
| repo-in-use | "last push to any branch" and "latest release" under Repo facts (live: newest commit date and the Releases sidebar). | Last push to any branch is within 180 days of the capture date. A missing or old release does not fail this check on its own. | required |
| bounded-scope | The issue body and the full comment thread. | The issue asks for one piece of work that a single pull request can deliver. Fail if any of these is true: (a) the body or a maintainer calls it an umbrella, tracking, or meta issue, or it lists sub-items meant to be split into separate PRs; (b) the thread shows the approach is still being debated and no maintainer has stated which approach to take; (c) a maintainer says the fix needs changes to core internals or a redesign; (d) it is a usage or support question with nothing to change in the repo; (e) the issue has two or more closed, unmerged PRs in its history and has been open more than 1 year. A short body, a checklist, or missing repro steps do not fail this check by themselves. | required |
| unclaimed | "this issue: assignees" and "linked PRs" under Repo facts, plus every PR link or claim comment in the Comments section. | All three hold: (1) assignees is `none`; (2) no OPEN pull request (linked, or mentioned in a comment, including PRs from forks) targets this issue; (3) no comment dated within 30 days of the capture date says the commenter is working on it or will take it, unless a later comment says that person stopped. In live mode on the Path Review repo, apply the scope.md house rule: classmates' claim comments do not count for part (3). | required |
| ai-policy-allows | The "contribution policy" line under Repo facts (live: CONTRIBUTING.md, AI_POLICY.md, and PR templates). | Fail only if the policy states the project does not accept, bans, or prohibits AI-generated or AI-assisted contributions. Conditions (disclose AI use, review and understand the code, test it, human review), discouragement without a ban, an AGENTS.md file, or no policy at all pass. | required |
| maintainer-engaged | The issue's "opened by" line and the author_association of each commenter. | The issue was opened by a maintainer, or a maintainer has commented in the thread. | preferred |
| newcomer-label | The issue's labels. | Carries a label such as `good first issue`, `easy`, or `help wanted`. | preferred |

## Verdict rule

Accept if every `required` check passes; reject if any `required` check
fails. `unclear` on a required check counts as fail, with one exception:
`ai-policy-allows` grades `pass` when no policy is found, because silence
is not a restriction. `preferred` checks never change the verdict; they
only rank accepted issues (more preferred passes ranks higher, then the
fit profile in scope.md in live mode).
