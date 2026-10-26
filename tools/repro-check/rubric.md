# Rubric: is this reproduction package ready to post?

Every check reads the package against the issue it belongs to. In eval
mode the package is the bundle; in live mode it is the draft comments
plus the live issue. "The issue's behavior" means the symptom the issue
describes (its error, wrong output, or missing effect) under the trigger
it describes.

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| claim-names-issue | The claim comment, read against the issue title and body. | The claim names at least one detail specific to this issue (its symptom, error text, function, file, command, or test name) and says what the author will do next. Fail if the claim could be pasted unchanged onto a different issue, or if it states a reproduction result that the repro report does not back. | required |
| environment-recorded | The repro report's environment record, read against any version, platform, or configuration the issue or its thread names as the target. | The report names the project version actually run (release, package version, or commit) and the runtime the behavior depends on (for example Python, Node, browser, or OS). If the issue body names the project version, platform, or configuration where the bug appears (including "the latest release" or "main"), the report's project version either matches it or the report says plainly how it differs. Fail if the project version is missing, or if the project version run differs from the issue body's stated target without the report saying so, even when the behavior still appears. A dependency version or platform suggested only in a thread comment does not set the target, so not matching it does not fail this check. | required |
| steps-rerunnable | The repro report's steps, from starting state to trigger. | A stranger with the recorded environment could trigger the behavior from the report plus the issue: every command, input, file, or setting the trigger needs is given literally, quoted from the issue, or pinned down exactly by pointing at content in the issue (for example "the issue's two format calls") or by a description precise enough that any stranger would build an equivalent input. Fail if a step that matters is only gestured at ("set up the project", "run it the usual way", "use my config") so the stranger would have to guess what was run, or if it depends on private data the report does not share. | required |
| behavior-matches-issue | The output excerpts, logs, error text, or test results in the repro report, read against the issue's described symptom and trigger. | The artifacts show the issue's behavior under the issue's trigger (same symptom, same code path or command), or, for a cannot-reproduce or partial attempt, show the commands the author actually ran with their real output and state plainly which part of the issue's trigger they could not reach. Fail if there is no artifact at all, if the artifact shows a different error, a different command, a different configuration, or an adjacent bug, or if the observed result is only asserted in prose. | required |
| outcome-honest | The report's stated conclusion (reproduced, not reproduced, partial), plus any root-cause or fix claims in the claim or report, read against the artifacts shown. | The conclusion says exactly what the artifacts show and no more. An evidenced cannot-reproduce or partial reproduction passes. Fail if the report claims a reproduction its artifacts do not show, presents a root cause or fix as confirmed without evidence, or hides a mismatch between what it ran and what the issue describes. | required |
| conventions-respected | The repo's contribution policy and AI-use policy (the repo-facts block in eval mode; CONTRIBUTING.md, AI policy files, and issue/PR templates live), read against the claim comment and repro report. | If the policy requires disclosing AI assistance, the claim or the report contains a statement disclosing AI use. If the policy bans AI-generated contributions, the package fails. If the repo states no such requirement, this check passes. | required |
| template-asks-covered | The bug-report template asks in the repo-facts block (live: the issue template), read against the repro report. | Every item the template asks a reporter to provide (for example version, OS, minimal steps) is present in the report. | preferred |

## Verdict rule

Accept (ready to post) if every `required` check passes; reject (hold)
if any `required` check fails. `unclear` on a required check counts as
fail. Exception for live claim-only drafts: checks whose evidence is
the repro report (environment-recorded, steps-rerunnable,
behavior-matches-issue, outcome-honest, and template-asks-covered)
grade `unclear` with "not yet applicable: claim-only draft" and are
left out of the verdict; the verdict then rests on claim-names-issue
and conventions-respected. `preferred` checks never change the verdict.
