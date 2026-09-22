---
name: issue-select
description: Grade a candidate open-source issue against a written rubric and decide whether it is worth taking as a first contribution.
---

# issue-select: rubric-driven first-issue grading

Grade one candidate issue to answer: should a newcomer take this as their
first contribution? Execute `rubric.md` check by check against gathered
evidence; do not decide from gut feel.

## Inputs

- **Live mode:** one or more GitHub issue URLs. Read `scope.md`, then gather
  evidence from the live repository using GitHub or the API.
- **Eval mode:** a snapshot bundle containing the issue, comments, and Repo
  facts. Use only that bundle; do not fetch anything else.

## Scope and rubric

In live mode, read `scope.md` before grading. It identifies allowed candidate
repositories, Path Review house rules, and the contributor fit profile. Scope
and fit can rank accepted issues but cannot change a rubric verdict. In eval
mode, ignore `scope.md`.

Read `rubric.md` and execute every check in its table. Each check must receive
a grade of `pass`, `fail`, or `unclear`, plus one concrete evidence fact or
quote. Apply the verdict rule in the rubric exactly. If the rule does not say
how to handle `unclear`, treat it as a fail.

## Workflow

1. In live mode, confirm the issue is in scope and note any house rules.
2. Read the rubric and list its checks.
3. Gather the evidence named by each check. In live mode, use the surfaces in
   `references/evidence-guide.md`; in eval mode, quote the snapshot bundle.
4. Grade every check, then apply the verdict rule to produce `accept` or
   `reject`. Preferred checks never gate the verdict.
5. When grading several live issues, rank accepted issues by the fit profile
   and state the one-line fit reason.

## Output format

Before the final block, a short readable summary is allowed. End with this
fenced JSON object and nothing after it:

```json
{
  "item": "<issue URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one fact or quote>"}
  ],
  "verdict": "accept|reject"
}
```

In eval mode, always emit this single-object form. For several live issues,
the final JSON block may hold an array of objects, with accepted issues first.

## Grading discipline

- Never grade a check without evidence: a date, count, name, label, or quote.
- The rubric decides. Note tensions in the summary, but do not override it.
- A claim comment is interpreted according to the applicable scope house rule.
