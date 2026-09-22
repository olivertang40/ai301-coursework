# Unit 1 — Issue Selection

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73

**Verdict output**

I ran the rubric in live mode on issues #73, #72, and #63. All three were accepted. I selected #73 because it has no recent claim comment, names the two files to change, and estimates 1–2 hours of work. Issue #72 was also accepted; #63 was accepted but has a fresh interest comment, which is non-blocking under the classroom house rule.

```json
{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73",
  "checks": [
    {"name": "repo-active", "grade": "pass", "evidence": "Human commits by Andrew Burke were made on 2026-09-16, within 180 days."},
    {"name": "not-archived", "grade": "pass", "evidence": "Repository metadata reports archived: false."},
    {"name": "maintainer-response", "grade": "unclear", "evidence": "The live evidence did not establish a five-issue maintainer-response sample."},
    {"name": "visible-adoption", "grade": "fail", "evidence": "Repository metadata reports 2 stars, below the preferred threshold of 50."},
    {"name": "bounded-change", "grade": "pass", "evidence": "The issue asks to make README.md and .env.example agree about the LLM API key and provider options."},
    {"name": "workable-spec", "grade": "pass", "evidence": "The issue identifies the conflicting OPENROUTER_API_KEY and LLM_PROVIDER text and names README.md and .env.example."},
    {"name": "no-stale-attempts", "grade": "pass", "evidence": "The issue opened on 2026-09-16, so it is not older than 365 days."},
    {"name": "ai-policy-compatible", "grade": "pass", "evidence": "No CONTRIBUTING.md or .github/CONTRIBUTING.md policy was present."},
    {"name": "unassigned", "grade": "pass", "evidence": "The issue assignees field is empty."},
    {"name": "no-active-pr", "grade": "pass", "evidence": "A search for open pull requests related to issue 73 returned none."},
    {"name": "no-recent-claim", "grade": "pass", "evidence": "The issue has no comments, so no recent claim comment exists."}
  ],
  "verdict": "accept"
}
```

## Eval iterations

**Run history**

- 0/1 scored items on the first smoke run.
- 1/1 after revising the bounded-change check.
- 17/20 on the first complete run.
- A targeted recheck matched the gold labels for `issue-15` and `issue-19`; `issue-04` was then included in the final complete run.
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

1. I chose #73 because it is a small documentation/configuration consistency fix with an estimated 1–2 hours of work, fitting a focused Unit 2 work session and my interest in debugging setup problems.
2. The verdict correctly identified a bounded, specified, unassigned issue with no open implementation PR. I also weighed that the task affects onboarding documentation, so the fix will help the next contributor configure the project correctly.
3. The issue currently has no assignee, linked PR, or claim comment. The anticipated difficulty is deciding the canonical key and provider wording; I will confirm the behavior in `core/config.py` before making the Unit 2 claim comment.
