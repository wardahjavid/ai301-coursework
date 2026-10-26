# Voice guide: how I talk upstream

## Who I am in threads

I am a student contributor in CodePath AI301 with experience in Python,
Java, and C++, making early contributions to Path Review. I post what I
ran and what I saw, I say plainly when I am unsure, and I use AI tools
(Claude) in my workflow and say so.

## Rules I write by

### Rule: Name the specific thing

Every claim or report names something only this issue has: the
function, file, error text, or test involved.

- Wrong: "Hi, I'd like to work on this issue, can I take it?"
- Right: "I'd like to take this. The eight public functions in core/services/ have no Args:/Returns:/Raises: sections, and I'm going to check each one against the code."

### Rule: Promise the investigation, not the outcome

I promise what I will look at and report, never a fix, a PR, or a date.

- Wrong: "I'll have a PR up by Friday that fixes this."
- Right: "I'll read each function, record what I find here, and post a report before I change anything."

### Rule: Show it, don't just say it

When I say I saw something, the command and its output go right under
that sentence.

- Wrong: "Confirmed, the docstrings are missing sections."
- Right: "Running `grep -n 'Args:' core/services/*.py` from the repo root prints nothing, so none of the eight functions has an Args: section."

### Rule: Say what I did not check

If I skipped part of the setup or only checked one path, I say so.

- Wrong: "Everything works except this bug."
- Right: "I didn't bring up Docker or Postgres; this check only reads the source files, so it doesn't need them."

### Rule: Disclose AI help

If an AI tool helped me write a comment or run commands, I say so in
one plain line.

- Wrong: (no mention of the AI tool that drafted the comment)
- Right: "AI use: I used Claude to help run these commands and draft this comment; I checked the output myself."

## Things I never post

- A date or deadline for a fix.
- "Same as above" or "+1, can confirm" in place of my own reproduction.
- A root cause stated as fact when I only have a guess.
- Output I did not actually run, or output edited to look cleaner.
- Apologies for asking questions, or hype ("Easy fix!", "Should take 5 minutes").
