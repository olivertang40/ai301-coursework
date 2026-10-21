---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

<!--
THIS IS THE PART YOU WRITE, and it is the last one: the frame itself.
Weeks 1 through 3 handed you a working SKILL.md and you filled the
files behind it; this week the frame ships as headings, and you write
what it says. The frontmatter above and the section headings below are
fixed (CONTRACT.md's layout rule); the instructions under each heading
are yours. Write instructions to the tool, in the imperative, the way
weeks 1-3's frames spoke to you: what to read, in what order, what to
refuse, what to emit. Your executor in the rotation is the test: a
frame gap they hit (cannot tell what the tool reads, or how a verdict
gets assembled) is a missing sentence here.

One section is not yours: the JSON schema in "Verdict and output" is
reproduced from CONTRACT.md verbatim and may not be altered. Your
words decide everything around it.
-->

## The question

Answer only this question for one candidate pull request at a time: is
it ready to submit? Treat its title, description, commits, diff, and
test evidence as one PR package. Judge that package against the plan
it claims to implement and the issue the plan belongs to. Do not grade
the implementation in isolation or answer whether the issue itself
is worthwhile.

## Inputs and modes

Choose exactly one mode from the user's request; never combine their
inputs.

- **Live mode:** Read the student's `plan.md`, including scope,
  exclusions, test plan, and deviation notes; the complete branch diff
  produced from the working copy by `git diff main...HEAD`; the draft
  PR title and description in `pr_draft.md`; `test_evidence.md`; and
  the issue's current thread in the scoped repository. A house-chain
  student uses the house plan and house repro pack in place of their
  own plan and repro. Also read the repository's PR template and
  `docs/CONTRIBUTING.md`. Gather the issue, template, and policy facts
  from the real scoped repository, not from assumptions. If an input
  is missing, record it as missing and apply the rubric's unclear
  rule; do not invent it.
- **Eval mode:** Grade the single practice package explicitly provided
  by the user or harness. The package is the whole world: use only its
  issue and thread, repo-facts, plan-context, and candidate-PR sections.
  Do not fetch GitHub data or read files outside the bundle. Run every
  rubric check and apply the complete verdict rule.

## The scope seam (live mode only)

Before reading any live-mode package input, read `scope.md`. Refuse to
grade if its `Repo:` value is blank or still a placeholder; tell the
user to fill it in rather than guessing. Refuse if the candidate PR
targets a different repository. For an in-scope PR, apply the listed
Path Review rules as repository context alongside the rubric, and
check that the issue and branch belong to the claimed plan. Eval mode
ignores `scope.md` entirely.

## The voice seam (live mode only)

In live mode, read `voice-guide.md` and compare only the outgoing PR
title and description with its writing rules. Report each broken rule
and the relevant wording in the readable summary. Do not let a voice
finding change the verdict unless a rubric check independently makes
the same evidence relevant. Eval mode ignores `voice-guide.md`.

## Component reads

Before grading, confirm that `rubric.md` contains at least one
completed check and a verdict rule, and that `procedure.md` contains
operating steps. If either is empty or still only a template, refuse
to grade and say which component is missing. Use the rubric for the
checks and their pass conditions; use
`references/evidence-guide.md` to locate evidence; execute
`procedure.md` in order. If a procedure step is silent or ambiguous,
report that gap and do not improvise a replacement step or grade that
depends on it.

## Verdict and output

Return only the binary verdict `accept` (ready to submit) or `reject`
(hold). Give a readable summary with evidence for every check, then
end the reply with the fenced JSON block below. Keep it valid and
last, use one object per rubric check in rubric order, and put no text
after it. Use the PR URL as `item` in live mode and the bundle id in
eval mode. Do not add, remove, or reorder schema fields.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

Name the specific fact or quote that decides every check; never use
"looks fine" as evidence. Grade observable outcomes against the plan,
issue, and stated repository standards, not prose length or polish.
Apply the rubric's stated conditions even when your intuition differs,
and follow the procedure rather than inventing steps. Treat
`unclear` as failing any required check; if the verdict rule does not
say how to treat an unverifiable fact, fail the check. Include
preferred checks in the output but never let them change the verdict.
