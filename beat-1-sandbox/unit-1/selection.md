# Unit 1 — Issue Selection

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/63

**Verdict output**

Issue #63 is accepted: it is a focused test-fixture correction with an observed failing assertion, no assignee, and no linked open pull request. A classmate's interest comment is a preferred-check concern only under the Path Review classroom house rule.

```json
{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/63",
  "checks": [
    {"name": "repo-active", "grade": "pass", "evidence": "Human commits by Andrew Burke were made on 2026-09-16, within 180 days."},
    {"name": "not-archived", "grade": "pass", "evidence": "Repository metadata reports archived: false."},
    {"name": "maintainer-response", "grade": "unclear", "evidence": "The live evidence did not establish a five-issue maintainer-response sample."},
    {"name": "visible-adoption", "grade": "fail", "evidence": "Repository metadata reports 2 stars, below the preferred threshold of 50."},
    {"name": "bounded-change", "grade": "pass", "evidence": "The issue narrows work to extending the README fixture or correcting its word-count assertion."},
    {"name": "workable-spec", "grade": "pass", "evidence": "pytest tests/unit/test_readme_scorer.py -q produces: assert 51 > 100."},
    {"name": "no-stale-attempts", "grade": "pass", "evidence": "The issue opened on 2026-09-10, so it is not older than 365 days."},
    {"name": "ai-policy-compatible", "grade": "pass", "evidence": "No CONTRIBUTING.md or .github/CONTRIBUTING.md policy was present."},
    {"name": "unassigned", "grade": "pass", "evidence": "The issue assignees field is empty."},
    {"name": "no-active-pr", "grade": "pass", "evidence": "A search for open pull requests related to issue 63 returned none."},
    {"name": "no-recent-claim", "grade": "fail", "evidence": "AliceKindle2 wrote on 2026-09-22: I'd like to investigate this one."}
  ],
  "verdict": "accept"
}
```

## Eval iterations

**Run history**

- 0/1 scored items on the first smoke run.
- 1/1 after revising the bounded-change check.
- 17/20 on the first complete run.
- A targeted three-item recheck validated revised scope and stale-attempt criteria.
- 18/20 scored items on the final complete run (PASS).

**Issue analysis**

`issue-12` was rejected by this rubric, matching its gold label of `reject`. The deciding source text was: “We do not accept AI-generated code or documentation.” The required `ai-policy-compatible` check failed despite otherwise positive activity, scope, and availability signals.

**Check rationale**

> `| no-stale-attempts | The issue age, comments, and linked PRs | An issue older than 365 days passes only if it does not show repeated abandoned claims or two or more closed, unmerged implementation attempts. | required |`

This check uses repeated abandoned attempts as evidence of hidden first-contribution difficulty.

**Trade-offs**

The check can reject an older issue that is technically solvable, favouring predictability over rescuing a complicated task. It changed `issue-15` from an incorrect acceptance to a correct rejection and the final run reached 18/20.

## Selection rationale

**Selection rationale**

1. I chose #63 because it is a small Python test-fixture problem with a clear failing assertion, fitting a focused Unit 2 work session and my interest in debugging and tests.
2. The verdict correctly identified a bounded, specified, unassigned issue with no open implementation PR. I also weighed that the issue gives two possible fixes, so I will inspect intended scorer behavior before choosing one.
3. A classmate recently expressed interest, creating some coordination ambiguity. Path Review policy says that comment is not a claim and credit attaches to the PR; I will still check the thread again before the Unit 2 claim comment.
