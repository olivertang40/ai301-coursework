# Rubric: is this pull request ready to submit?

<!--
THIS IS THE PART YOU WRITE (fourth week running; this is the rubric's
final form in the sandbox). Your frame in SKILL.md executes whatever
checks you define here, via your procedure.md. It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the diff read against the plan's scope, the test
     evidence read against the plan's test plan, the description read
     against the diff, the repo-facts block's template asks) or a
     location from your references/evidence-guide.md. "The PR" is not
     a source; "the diff's changed files read against the plan's
     stated boundary" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself
     (does the diff fall inside the plan plus its deviation notes? is
     the claimed evidence observable?), never the write-up's shape
     (how long the description is, how many commits there are).
     Structure-shaped checks are what make graders disagree with
     themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (submit) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. State the `unclear`
   treatment explicitly: the frame here is YOUR SKILL.md, so a rubric
   that stays silent is only covered if your frame's grading
   discipline says what happens (the contract's own default is that
   an unverifiable claim fails).

Cover what actually gets bad PRs submitted. The failure families the
lecture named ARE the harness's scoring categories, same names as the
eval README: silent drift (the diff silently does more or less than
the posted plan, or the description claims fidelity the diff
contradicts), not tested (the evidence proves nothing observable, or
the repo's own checks were never run), unreviewable (debris or
unrelated hunks bury the change), and standards wall (the repo's
stated template and disclosure asks are ignored). Your evidence
guide's four headings map onto these one to one (plan fidelity =
silent drift, test evidence = not tested, diff quality =
unreviewable, standards and comms = standards wall), and the category
floor is scored on exactly these names plus clear accept. A rubric
that ignores a category will fail the eval packages built around
that category. And remember the honest-outcome
rule, fourth week running: a PR that honestly discloses a shortfall
can be ready; a rubric that equates "less than everything" with
"hold" fails the set.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Silent drift — plan fidelity | Compare the plan's files, scope, exclusions, expected behavior, and deviation notes with the full diff; compare every material claim in the PR title and description with the diff and plan. | Every changed behavior and file is within the plan or is tied to a specific, explained deviation; no planned, in-scope outcome is silently omitted; and the title and description do not claim work or behavior the diff does not deliver. An explicit, honest deviation or limitation is not silent drift by itself. | required |
| Not tested — test evidence | Compare `test_evidence.md` (or the bundle's test-evidence section) with the plan's test plan and repro steps; verify that outputs identify what ran and what happened, including each applicable repository check and its result. | Evidence makes the primary before/after repro behavior and expected outcome observable and reports test/check outcomes truthfully, including failures or an expected no-tests result with its reason. For planned control cases, an explicit reported outcome (such as "unchanged") is sufficient when the primary repro and relevant suite results are observable; do not demand a separate transcript for every control. A claim such as "tests pass" without results, a planned primary check with no evidence or explanation, or a test unrelated to the planned behavior fails. A reported failure is evidence, not proof of a pass; apply repository policy to its outcome in the standards check. | required |
| Unreviewable — diff quality | Inspect the full diff and commit list for the implementation, unrelated changes, generated/debug artifacts, dead or commented-out code, and formatting churn that obscures the planned change. | A reviewer can identify the planned change and its effects in the diff; unrelated hunks or debris do not materially obscure or expand it. Do not fail merely for commit count, diff size, or style preference when the change remains reviewable and in scope. | required |
| Standards wall — repo standards and communication | Compare the draft title and description with every applicable section and checklist item in the repo's PR template; compare requested checks, branch/issue expectations, disclosure requirements, and thread direction with the PR/package and the repo's stated contribution policy. In eval, use only the package's repo-facts and thread. | The PR uses and substantively completes the template, links the correct issue, follows explicit repo policy and maintainer direction, and does not omit a required disclosure or required green check. Do not invent a disclosure rule absent from policy. An honestly reported failure satisfies transparency but does not satisfy a policy that explicitly requires that check to pass. | required |

## Verdict rule

Accept only when every required check passes. A fail or unclear on any
required check means reject; treat unclear as fail because the
submission is not verifiable. Preferred checks, if added later, are
reported but never affect the verdict. Do not reject an honestly
disclosed shortfall solely because it is incomplete: reject only when
the shortfall fails a stated required check or violates an explicit
repository requirement.
