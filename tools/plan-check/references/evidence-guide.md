# Evidence guide: where evidence lives in a plan package

Eval bundle layout (top to bottom): header (`source`, `captured`),
`## Repo facts`, `## Issue`, `## Thread highlights`, `## Repro
evidence`, `## Candidate plan`, `## Candidate plan comment`. The `.json`
twin has the same fields. In live mode the same families live on the
GitHub issue page, in the student's posted repro comment, in the
repo's CONTRIBUTING.md / AI_POLICY.md, and in the drafts `plan.md` and
`comment.md`.

## Diagnosis and grounding

- **Where it lives:** in the candidate plan, the first line labeled
  "Cause:" or "Diagnosis:" (sometimes the opening paragraph). The
  behavior that cause has to explain is in the `## Repro evidence`
  block: the numbered steps, the artifacts (output, stack traces, exit
  codes, timing tables), the **Control** runs, and the Expected/Actual
  lines. In live mode, it's the student's posted repro comment, or the
  repro evidence quoted in `plan.md`.
- **What good looks like:** the stated cause predicts every step and
  every control: it is present where the bug shows and absent where
  the control passes. A control that shows the bug without the blamed
  component, or shows the blamed component running fine, means the
  cause is wrong, however confident the plan is or however many thread
  comments agree with it. The fix targets that cause, not a workaround
  for its symptom.

## Scope

- **Where it lives:** the plan's "Change:"/"Scope:" paragraph, its
  explicit "In scope" / "Not in scope" (or "Out:") lines, and every
  numbered approach step. Watch for "also", "while I'm here", "take
  the opportunity to", and lists of several fronts.
- **What good looks like:** one change at the site the repro isolates,
  plus its regression test. Related improvements are named only as
  deferred or not in scope. A drive-by rewrite commits to upgrades,
  migrations, new options, new UI, framework changes, or ports to
  sibling components alongside (or wrapped around) the core fix.

## Executability

- **Where it lives:** file paths, function names, and code sites in
  the plan's change and approach sections. The chosen mechanism is
  usually the verb in the change line ("add `--` before the path",
  "clamp with saturating_sub").
- **What good looks like:** a named location plus one committed
  mechanism, so a stranger could open the file and start. Not
  executable: "somewhere", "investigate the X stack", "A or B,
  whichever is easier", "not sure which layer", "profile and
  optimize" with no target.

## Test plan

- **Where it lives:** the plan's "Test:"/"Test plan:" section, read
  next to the repro evidence's steps and Expected line.
- **What good looks like:** it re-runs the repro (or a named
  regression test of that case) and states the expected observable
  result: an exit code, specific output, a color change, a named test
  passing, a control still behaving. Vague: "run the full test suite",
  "CI green", "should feel fast", "nothing else should break", with no
  outcome specific to the fix.

## Honesty

- **Where it lives:** "Risk", "Unknowns", "Open question", or
  "Deviations" lines in the plan, and qualifiers in the approach ("I
  have verified X; I will verify Y"). In live mode, an honest mid-build
  deviation goes under `## Deviations` in `plan.md`, and a follow-up
  comment goes on the issue if the posted plan is no longer true.
- **What good looks like:** verified and unverified claims are kept
  apart. Untested platforms, unmeasured costs, and deferred variants
  are named as such. False confidence asserts something the evidence
  doesn't show ("this is definitely the only call site") or hides a
  deferral.

## Comms

- **Where it lives (thread):** `## Thread highlights`. Each line
  carries the author's role in parentheses (OWNER, MEMBER,
  COLLABORATOR, CONTRIBUTOR, NONE). Maintainer direction is a comment
  from OWNER/MEMBER/COLLABORATOR, or the maintainer who opened the
  issue, that isolates a culprit, proposes or rejects an approach, or
  posts a patch. Also watch for mentions of open or prior PRs. In live
  mode, use the issue thread and its author-association badges.
- **Where it lives (conventions):** the `## Repo facts` block's
  "bug reports" and "contribution policy" lines. Read the AI policy
  wording closely: does disclosure apply to "any form" or to issues
  and comments, or only to pull requests? Is there an own-words rule
  for comments? In live mode, read CONTRIBUTING.md and AI_POLICY.md in
  the repo.
- **What good looks like:** the plan comment names the maintainer's
  direction or open PR and follows it, or explains why it differs. It
  doesn't re-propose a rejected approach or silently swap in a
  workaround. Where the repo requires AI disclosure for comments or for
  any form of contribution, the comment states that AI was used and
  how much. Boilerplate that ignores the thread fails, however polite
  it is.
