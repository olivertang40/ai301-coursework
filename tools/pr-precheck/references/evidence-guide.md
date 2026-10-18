# Evidence guide: where evidence lives in a PR package

<!--
THIS IS THE PART YOU WRITE (third week running: the map stays in your
hands). Your tool uses this guide as its map: for every kind of
evidence a rubric check names, this file says WHERE to find it in a PR
package and WHAT GOOD LOOKS LIKE when you do.

The four families below are the harness's failure categories under
the names the eval README uses: plan fidelity = silent-drift, test
evidence = not-tested, diff quality = unreviewable, standards and
comms = standards-wall. A package that fails none of them is a
clear-accept. Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the plan-context block's scope pair and test
  plan, the candidate PR's diff, commits, description, or
  test-evidence section, the repo-facts block's template asks and
  stated policy). In live mode (where in your working copy and on
  GitHub: your plan.md and its deviation notes, your branch's diff,
  your draft title and description, your captured test output, the
  repo's PR template and CONTRIBUTING.md).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("every changed file falls inside the
  plan's stated boundary or a deviation note") over adjectives ("the
  diff is clean").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts three ways: your
procedure says WHEN to gather each family, this guide says WHERE, and
your SKILL.md says the tool reads both. Write the map you wish your
executor had.
-->

## Plan fidelity (harness category: silent-drift)

**Eval:** Use the plan-context scope, exclusions, named files,
expected behavior, and deviation notes; compare them with the
candidate PR's unified diff and claims in its title and description.
**Live:** Use `plan.md` and its deviation notes beside the complete
`git diff main...HEAD` from the working copy, then check title and
description in `pr_draft.md` against the same diff. A house-chain
submission uses the house plan and repro pack. Good evidence shows
each changed file and behavior within the agreed boundary or connected
to a specific deviation, and each material PR claim borne out by the
diff. Unexplained omissions and overclaims are drift; an honest,
explicit deviation is not silent.

<!-- Where the plan states its scope, boundary, and deviation notes,
and where the diff shows what actually changed. What it means for a
diff to match the plan, for an honest deviation to re-tie a mismatch,
and what silent drift looks like in each direction (more than the
plan, or less with no note). The description's fidelity claims read
against the diff live here too: a description claiming more or less
than the diff delivers is silent drift, not a comms problem. -->

## Test evidence (harness category: not-tested)

**Eval:** Use the plan-context test plan and repro steps beside the
candidate PR's test-evidence section. Check command/step, expected
result, and actual output/result as a set. **Live:** Use the test plan
in `plan.md` beside `test_evidence.md`, including the before result
(from `main` or retained repro output), after result on the branch,
and each check required by the PR template or `docs/CONTRIBUTING.md`.
Good evidence makes the target behavior observable and reports
commands and outcomes truthfully. A visible failure or an expected
no-tests result with its reason is evidence of what happened, not a
claim of success; an unsupported "passes" statement is not evidence.
For planned controls, an explicit outcome such as "unchanged" can
support the check when the primary repro and relevant suite result
are observable; a separate transcript for every control is not
required.

<!-- Where the PR shows its proof: the test-evidence section's
before/after against the plan's test plan and the reproduction's own
steps, and the outcome of the repo's own checks or suite. What
decisive looks like (an observable behavior named, the expected-after
stated, the checks' outcome visible) next to "tests pass". -->

## Diff quality (harness category: unreviewable)

**Eval:** Inspect the complete candidate PR diff and commit list.
**Live:** Inspect the complete branch diff from `git diff main...HEAD`
and its commit list. Locate the behavior implementing the plan and
look for unrelated changes, debug/generated artifacts, dead or
commented-out code, and avoidable churn that hides the fix. Good
evidence identifies the in-scope implementation and any material
obstruction; size or commit count alone says nothing about
reviewability.

<!-- Where the change itself lives: the unified diff and the commit
list. What a reviewable change looks like (the fix visible, nothing
unrelated riding along) and the debris tells: debug leftovers, dead
code, commented-out blocks, formatting churn, drive-by edits. -->

## Standards and comms (harness category: standards-wall)

**Eval:** Use the package's repo-facts PR-template asks and stated
contribution policy, including AI-use policy if one is explicitly
stated, alongside the PR title, description, test evidence, branch/
issue facts, and thread highlights. **Live:** Use the repository's
`.github/PULL_REQUEST_TEMPLATE.md`, `docs/CONTRIBUTING.md`, current
issue thread, and `pr_draft.md`, plus test outcomes. Good evidence
shows substantive responses to applicable template sections,
accurate issue linkage, compliance with explicit policy and
maintainer direction, and any required disclosure. Do not infer a
disclosure requirement when the repository does not state one.

<!-- Where the repo states its asks (the repo-facts block's PR
template sections, contributing instructions, and stated policy,
including AI-use disclosure) and where the PR honors them: the
stated sections filled with real content, the disclosure present,
explicit maintainer direction in the thread engaged. What compliant
looks like next to boilerplate or a visibly ignored ask. (Whether
the description's claims match the diff is plan fidelity, above.) -->
