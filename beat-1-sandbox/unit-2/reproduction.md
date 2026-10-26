# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

wardahjavid

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/48#issuecomment-6412501256

Hi! I'd like to take #48. The eight public functions in `core/services/` (`create_profile`, `get_profile`, `update_profile` and `delete_profile` in `profile_service.py`; `create_review`, `get_review`, `list_reviews` and `process_review` in `review_service.py`) have short, prose-only docstrings with no `Args:`, `Returns:` or `Raises:` sections.

Next, I'll check each docstring against what the code does, including the two error paths the issue calls out: `delete_profile` rolls back and re-raises, and `process_review` sets the review to `failed` and returns. I'll post a reproduction report here before I change anything.

AI use: I'm using Claude to help run commands and draft my comments. I read the code and check the output myself.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/48#issuecomment-6412520212

Reproduction report for #48. Result: reproduced on `main` at commit `2f4e82f52efbcfcc57d65b3fa5348672163ca088`.

**Environment**

- Path Review `main` at `2f4e82f52efbcfcc57d65b3fa5348672163ca088` (fresh clone, no local changes)
- Python 3.13.17 on Linux (x86_64). The project asks for `requires-python = ">=3.11"`; this check only parses source files, so the version difference doesn't matter here.
- No dependencies installed and no Docker/Postgres: the steps below only read `core/services/*.py` with the standard library.

**Steps** (from the repo root)

```
git clone https://github.com/codepath/pathreview-ai301-fa26-s3.git
cd pathreview-ai301-fa26-s3
git checkout 2f4e82f52efbcfcc57d65b3fa5348672163ca088
```

1. Search the two files for the section headers the issue asks for:

```
$ grep -nE "Args:|Returns:|Raises:" core/services/profile_service.py core/services/review_service.py; echo "exit=$?"
exit=1
```

No matches.

2. Print every public function's docstring:

```
$ python3 - <<'EOF'
import ast
for path in ["core/services/profile_service.py", "core/services/review_service.py"]:
    tree = ast.parse(open(path).read())
    for node in tree.body:
        if isinstance(node, (ast.FunctionDef, ast.AsyncFunctionDef)) and not node.name.startswith("_"):
            doc = (ast.get_docstring(node) or "").replace("\n", " ")
            print(f"{path}::{node.name}: {doc!r}")
EOF
core/services/profile_service.py::create_profile: 'Create a new profile for a user.'
core/services/profile_service.py::get_profile: 'Get a profile by ID, checking ownership.'
core/services/profile_service.py::update_profile: 'Update a profile, checking ownership.'
core/services/profile_service.py::delete_profile: 'Delete a profile and cascade delete reviews and ingested sources. Returns True if deleted, False if not found.'
core/services/review_service.py::create_review: 'Create a new review with status="pending".'
core/services/review_service.py::get_review: "Get a review by ID, checking that it belongs to the user's profile."
core/services/review_service.py::list_reviews: 'List reviews for a user with pagination. Returns (reviews, total_count).'
core/services/review_service.py::process_review: 'Background task to process a review. Steps: 1. Set status="processing" 2. Run ingestion pipeline on profile\'s sources 3. Run agent orchestration 4. Run RAG retrieval + generation 5. Run safety checks on output 6. Set status="complete", store sections in review.sections 7. On exception: set status="failed", log error'
```

That is eight public functions, and none of them has an `Args:`, `Returns:` or `Raises:` section. `delete_profile` and `list_reviews` mention a return value in plain prose only.

3. The two error paths the issue names, as they appear in the code:

`core/services/profile_service.py`, lines 109-112 (`delete_profile`):

```python
    except Exception as exc:
        log.error("profile_cascade_delete_failed", profile_id=str(profile_id), error=str(exc))
        await db.rollback()
        raise
```

`core/services/review_service.py`, lines 183-195 (`process_review`):

```python
    except Exception as exc:
        log.error("review_processing_failed", review_id=str(review_id), error=str(exc))
        try:
            stmt = select(Review).where(Review.id == review_id)
            result = await db.execute(stmt)
            review = result.scalars().first()
            if review:
                review.status = "failed"
                review.updated_at = datetime.utcnow()
                db.add(review)
                await db.commit()
        except Exception as e:
            log.error("review_status_update_failed", review_id=str(review_id), error=str(e))
```

The exception is logged, the review is set to `failed`, and nothing is re-raised. A second failure while saving that status is only logged.

**Expected** (per the issue): each public function's docstring has the `Args:`/`Returns:`/`Raises:` sections that apply, matching the code (for example, a `Raises:` entry for `delete_profile`'s re-raise, and none for `process_review`, which swallows the exception).

**Actual:** none of the eight docstrings has any of these sections.

**Not checked yet:** I haven't confirmed which exceptions the database calls in each function can raise. I'll trace that before I write the `Raises:` entries.

AI use: I used Claude to help run these commands and draft this report. The output above is from my run, and I checked it against the source.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. Full run (first rubric): "agreement: 16/20 scored items  (bar: 18/20: below the bar)". All categories matched except "clear-accept 4/8"; pkg-01, pkg-05, pkg-09 and pkg-12 were rejected against gold accept.
2. Partial run, `--only pkg-01,pkg-05,pkg-09,pkg-12,pkg-02,pkg-08,pkg-16,pkg-17,pkg-06,pkg-18,pkg-19,pkg-13` after loosening environment-recorded, steps-rerunnable and behavior-matches-issue: "agreement: 11/12 scored items". The four accepts now agreed, but the canary pkg-16 flipped: "pkg-16  reject  accept   NO     graded accept".
3. Partial run, `--only pkg-16,pkg-01,pkg-03,pkg-05,pkg-09,pkg-12` after tightening environment-recorded again for the project version: "agreement: 6/6 scored items".
4. Confirming full run, saved as eval-run.txt: "agreement: 20/20 scored items  (bar: 18/20: PASS)", with "categories: clear-accept 8/8  disclosure 1/1  no-evidence 4/4  unfollowable-comms 3/3  wrong-target 4/4".

**Package analysis**

pkg-16 (pandas-dev/pandas#66656): my final rubric decided reject; the gold label is reject (category wrong-target).
The report reproduces the crash cleanly ("ValueError: Length of new names must be 1, got 3"), so behavior-matches-issue and steps-rerunnable pass. What sinks it is the environment. The issue says "The reporter confirmed the bug on the latest version and on the main branch", but the report ran "pandas 1.5.3 (pip), Python 3.10.12, Ubuntu 22.04 (x86_64)" and never says that this is an old release rather than the target. In run 2, my loosened environment check let it through, because its evidence read: "differs from the latest/main target without saying so, but the crash still reproduces so the difference does not explain the result." That was the wrong reading: a silent deviation is unfaithful even when the symptom appears, because a maintainer cannot tell whether the bug still exists on main. After I rewrote the check to fail any unstated project-version difference "even when the behavior still appears", run 3 graded it reject again.

**Check rationale**

Check: environment-recorded. Pass condition as it now reads: "The report names the project version actually run (release, package version, or commit) and the runtime the behavior depends on (for example Python, Node, browser, or OS). If the issue body names the project version, platform, or configuration where the bug appears (including "the latest release" or "main"), the report's project version either matches it or the report says plainly how it differs. Fail if the project version is missing, or if the project version run differs from the issue body's stated target without the report saying so, even when the behavior still appears. A dependency version or platform suggested only in a thread comment does not set the target, so not matching it does not fail this check."
Why it reads this way: the first version failed any difference from "any version, platform, or configuration the issue or its thread names". That rejected the faithful pkg-01, whose evidence read "Report ran multidict 6.6.0 while thread names a multidict 6.5.0 regression", even though the thread comment was only a guess at a cause. I then loosened it to fail only when the difference "could explain the result", which let pkg-16 through. The final form splits the two cases: the issue body sets the target for the project's own version, and that must match or be called out, while thread-level dependency guesses do not set the target.

**Trade-offs**

The canary I re-ran: loosening this check flipped pkg-16 from reject to accept in run 2 ("pkg-16  reject  accept   NO     graded accept"), so I tightened the project-version rule and re-ran pkg-16 together with the five clear-accepts the change could touch (pkg-01, pkg-03, pkg-05, pkg-09, pkg-12): "agreement: 6/6 scored items". What the final check gives up: a report run on a different dependency version from the one a thread comment blames is accepted, even if that dependency is the real cause. A maintainer may still have to ask for the dependency version. I accept that miss, because a thread guess is not the issue's stated target, and failing on it rejected a faithful reproduction (pkg-01).

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
