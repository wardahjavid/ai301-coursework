# Rubric: is this a good first issue?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Concrete outcome | Issue title, body, and maintainer comments describing the requested change or incorrect behavior | Pass if the issue states a specific behavior to change, bug to fix, or output to produce. Fail if the requested result cannot be identified from the available issue evidence. | required |
| Bounded scope | Issue body, comments, referenced components/files, and repo facts describing the work involved | Pass if the issue describes one coherent change or one closely related set of changes. Fail if it explicitly requires a repository-wide migration, major redesign, broad refactor, or coordinated changes across more than two independent subsystems. | required |
| Verifiable result | Reproduction steps, examples, expected behavior, tests, acceptance criteria, or another stated way to tell when the issue is fixed | Pass if the available evidence gives at least one objective way to determine whether the change works. Fail if success would depend only on subjective judgment or unstated expectations. | required |
| No unresolved blocker | Issue body and comments for dependencies, pending decisions, missing information, inaccessible services, credentials, or maintainer action | Pass if no unresolved dependency prevents a contributor from beginning and testing the work. Fail if the issue explicitly depends on an unanswered design decision, unavailable private resource, missing credentials, or another unfinished issue that must be completed first. | required |
| Repository-local work | Issue body, comments, and repo facts describing required systems and dependencies | Pass if the contribution can be implemented and meaningfully verified using the repository and resources available to a normal contributor. Fail if completion requires access to a private production environment, organization-only system, proprietary data, or another inaccessible resource. | required |
| Starting-point evidence | File names, module/component names, stack traces, reproduction steps, code references, linked tests, or other concrete pointers | Pass if at least one concrete starting point is provided. Mark unclear if none is provided. | preferred |
| Existing verification support | Existing or requested tests, reproducible commands, screenshots/examples, or clearly stated expected output | Pass if the issue provides a strong verification path that would make implementation easier for a newcomer. Mark unclear if the issue does not provide this evidence. | preferred |

## Verdict rule

Accept an issue only if every `required` check passes.

If any required check is `fail` or `unclear`, reject the issue.

`preferred` checks never change an accept/reject verdict. They are used only to rank issues that already pass every required check.

When several issues are accepted, prefer issues with more passing preferred checks. In live mode, use the fit profile in `scope.md` as the final ranking factor among accepted issues.
