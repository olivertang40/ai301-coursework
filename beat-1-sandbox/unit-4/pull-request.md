# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your pull request

**Pull request**

Not opened yet. The live precheck returned `reject` because the
required frontend test timed out twice. A later `make check &&
make test-unit` run passed (Ruff, Black with 110 files unchanged,
mypy, and 375 unit tests passed with 53 xfailed). The issue #73 diff
is limited to `.env.example`, so I am not changing an unrelated
frontend test. `npm test -- --run` still times out in
`ProfileForm > validates portfolio URL character limit`; I disclosed
it rather than marking the CI checklist green. I tried to run the
repository's GitHub Actions workflow on the branch for Linux CI
evidence, but GitHub denied workflow dispatch with HTTP 403 because
this account does not have repository-admin rights. I am holding the
PR until CI is green or a maintainer confirms an exception.

**Branch**

`fix/73-env-example-openrouter-key`

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. The first full-run attempt failed before producing results because
   Windows decoded Claude's UTF-8 output as GBK; it has no score.
2. Retried the full run with Python UTF-8 mode: **19/20** agreed
   (category floor passed).
3. Regraded `pkg-19` with `--only`: **0/1** agreed.
4. Regraded `pkg-19,pkg-02` as the clear-accept canary run: **2/2**
   agreed.
5. Final full confirmation: **20/20** agreed; categories were
   clear-accept 7/7, not-tested 4/4, silent-drift 4/4,
   standards-wall 2/2, unreviewable 3/3. This matches the final
   harness-generated `eval-run.txt`.

**Package analysis**

`pkg-19`: the first full run's rubric verdict was **reject**, while the
gold label was **accept**. The test-evidence check failed because the
planned controls were reported as unchanged without separate output
transcripts, even though the issue repro had observable before/after
output and `go test ./...` passed. I revised the check to accept
reported control outcomes when the primary repro and relevant suite
results are observable; the targeted rerun and final full run both
graded `pkg-19` **accept**.

**Check rationale**

> Not tested — test evidence | Compare `test_evidence.md` (or the
> bundle's test-evidence section) with the plan's test plan and repro
> steps; verify that outputs identify what ran and what happened,
> including each applicable repository check and its result. |
> Evidence makes the primary before/after repro behavior and expected
> outcome observable and reports test/check outcomes truthfully,
> including failures or an expected no-tests result with its reason.
> For planned control cases, an explicit reported outcome (such as
> "unchanged") is sufficient when the primary repro and relevant
> suite results are observable; do not demand a separate transcript
> for every control. A claim such as "tests pass" without results, a
> planned primary check with no evidence or explanation, or a test
> unrelated to the planned behavior fails. A reported failure is
> evidence, not proof of a pass; apply repository policy to its
> outcome in the standards check. | required

I revised this condition after `pkg-19` exposed an overly strict
requirement: controls were explicitly reported unchanged, while the
main repro and full suite results were visible. The revision prevents
that paperwork gap from outweighing observable evidence, without
accepting an unsupported primary test claim.

**Trade-offs**

This revision changes `pkg-19` from reject to accept. I reran the
already-agreeing clear-accept `pkg-02` as a canary with `--only`;
it remained accept. The test check still requires observable primary
before/after behavior and relevant suite results, so a summary of
controls cannot substitute for missing evidence of the fix itself.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.
