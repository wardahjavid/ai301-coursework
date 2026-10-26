# Evidence guide: where proof lives in a reproduction package

This is the map for every check in rubric.md: where to look for each
kind of proof, in an eval bundle and in live mode, and what good looks
like once you find it.

## Environment

- Where it lives:
  - Eval bundle: the repro report's environment line or block (often
    starting "Environment:"). Read it against the issue body, the thread
    highlights (which often name the version or platform where the bug
    appears), and the repo-facts block's "latest release".
  - Live: the draft repro comment's environment section, read against
    the issue body, its comment thread, and the repo's setup docs
    (README, docs/SETUP.md, pyproject.toml or package.json for the
    required runtime version).
- What good looks like: the report names the project version actually
  run (release number, package version, or commit hash) plus the
  runtime and OS the behavior depends on. When the issue says the bug
  appears on a particular version, platform, or configuration, the
  report either matches it or states the difference in plain words.
  A version that silently differs from the issue's target is not a
  sufficient record.

## Steps

- Where it lives:
  - Eval bundle: the repro report's steps, commands, and code blocks,
    from the first setup command to the command that triggers the
    behavior.
  - Live: the same sections of the draft repro comment.
- What good looks like: a stranger with the recorded environment can
  copy the commands or inputs in order and reach the trigger without
  guessing. Every input that matters (a command, a config value, a
  file's contents, a request body) appears literally or is quoted from
  the issue. A step that only describes an action ("install the
  project", "run my script", "use the attached config" when nothing is
  attached) is a gap. Length does not matter: one exact command can be
  complete, and ten vague steps can be unfollowable.

## Behavior shown

- Where it lives:
  - Eval bundle: output excerpts, error text, stack traces, test
    results, or screenshots described in the repro report, read
    against the symptom and trigger in the issue body.
  - Live: the same artifacts in the draft repro comment, read against
    the live issue body and any reproduction the issue author gave.
- What good looks like: the artifact shows the issue's symptom under
  the issue's trigger: the same error, the same wrong value, the same
  missing effect, reached through the same command or code path. A
  control run (the same command without the triggering condition) that
  behaves correctly strengthens it. An artifact that shows a different
  error, a different command, a different setting, or a neighbouring
  bug is the wrong target, however clean it looks. A sentence saying
  "I saw the bug" with no artifact shows nothing.

## Honesty

- Where it lives:
  - Eval bundle: the repro report's conclusion ("Reproduced", "Could not
    reproduce", "Actual:"), plus any root-cause or fix statements in the
    claim comment or report, set beside the artifacts that are supposed
    to back them.
  - Live: the same statements in the drafts.
- What good looks like: every claim has an artifact under it. "Could
  not reproduce" with the commands run and the correct output shown is
  an honest, complete result. A report that says "reproduced" while
  its output shows something else, presents a guessed root cause as
  confirmed, or skips over a difference between what it ran and what
  the issue describes is claiming more than its evidence shows.

## Comms

- Where it lives:
  - Eval bundle: the repo-facts block's "contribution policy" line
    (including any AI-use policy) and "bug reports" template asks, read
    against the claim comment and repro report; the claim comment read
    against the issue title and body.
  - Live: CONTRIBUTING.md (repo root, docs/, or .github/), any
    AI_POLICY.md or similar file, the issue and PR templates in
    .github/, and the scope.md house rules, read against the drafts.
- What good looks like: the claim names something specific to this
  issue (an error, a function, a command, a test name) and says what
  the author will do next, rather than generic "can I work on this?"
  boilerplate. When the repo requires AI-use disclosure, the claim or
  report says plainly that AI assistance was used. When the repo bans
  AI-generated contributions, the package is not ready. The template's
  asks (version, OS, minimal steps) are answered somewhere in the
  report.
