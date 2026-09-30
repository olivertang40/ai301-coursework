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

[Your GitHub username, exactly as it appears on your profile — no `@`, no profile URL. Your
comments upstream are identified by this name.]

---

## Posted upstream

**Claim comment**

[Link to the comment where you claimed the issue. Use the comment's own permalink, not the
issue page on its own. **Then paste the text of that comment underneath the link** — the
pasted text is what this field is graded on, so copy across what you actually posted.]

**Reproduction comment**

[Link to the comment where you posted your reproduction. It must record the environment
(OS, relevant versions, code state), steps a stranger could follow, and what you observed.
**Then paste the text of that comment underneath the link** — the pasted text is what this
field is graded on, so copy across what you actually posted.]

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

Full run 1 — 14/20. Categories: clear-accept 2/8, disclosure 1/1, no-evidence 4/4,
unfollowable-comms 3/3, wrong-target 4/4. Every one of the six disagreements was a false
reject on a clear-accept package.

Partial `--only` run (pkg-01, pkg-03, pkg-05, pkg-09, pkg-10, pkg-12 plus canaries
pkg-06, pkg-16, pkg-18, pkg-19, pkg-20) — 9/11. pkg-01, pkg-03, pkg-10 and pkg-12 flipped
to agree; every canary held.

Partial `--only` run (pkg-05, pkg-09 plus wrong-target and floor canaries) — 10/11.
pkg-05 fixed, wrong-target stayed 4/4.

Partial `--only` run (pkg-09 plus canaries) — 10/11. pkg-09's behavior check passed, but
its steps check still failed.

Partial `--only` run (pkg-09, pkg-18, pkg-06 plus canaries) — 8/10. pkg-09 fixed, but the
same edit flipped pkg-05 and pkg-10 back to reject. The canary rule caught the regression
before a full run.

Partial `--only` run (all accept-family packages plus pkg-18, pkg-20) — 10/11. pkg-05,
pkg-09, pkg-10 and pkg-12 all agreeing; only pkg-05's claims check left.

Partial `--only` run (pkg-05 plus every claims-dependent canary: pkg-02, pkg-06, pkg-13,
pkg-14, pkg-15, pkg-16, pkg-17, pkg-19, pkg-20) — 11/11.

Full run 2 (confirming, written to `eval-run.txt`) — **19/20**. Categories: clear-accept
7/8, disclosure 1/1, no-evidence 4/4, unfollowable-comms 3/3, wrong-target 4/4.

**Package analysis**

`pkg-05` (conda/conda#16543). My rubric decided **reject**; the gold label is **accept**.

The package reproduces the issue with a *minimal* `env.yml` carrying a `category:` section,
rather than the conda-lock environment URL the issue used, and shows the
`EnvironmentSectionNotValid` warning printed above the JSON plus a `python3 -m json.tool`
control that fails with `Expecting value: line 1 column 1 (char 1)`. That is the issue's
exact behavior, demonstrated on a smaller input.

My rubric read it as a reject for two reasons, both of which were my error rather than the
package's. Early runs failed it on `Steps replayable` and `Correct issue behavior`, because
those checks compared the report's *input* with the issue's input and treated any
difference as a deviation — which silently outlawed minimal reproduction, the thing a
maintainer most wants. In the final run it failed only on `Claims stay within evidence`,
which read the claim comment's "with `--json` every human-readable message should be routed
to stderr" as an unsupported generalization. It is not a factual claim at all; it is a
statement of expected behavior, and the issue itself asks for exactly that fix. The lesson
is that a check aimed at over-claiming has to separate assertions of fact from statements
of what the software ought to do, or it punishes a report for agreeing with the issue.

**Check rationale**

From the `rubric.md` uploaded to `tools/repro-check/`, the `Correct issue behavior` check
now reads:

> Pass if the artifact shows the behavior the issue describes. A simplified or minimal
> input that still produces that behavior is a legitimate reproduction, not a deviation.
> Also pass a cannot-reproduce report whose attempt was aimed at the issue's behavior,
> states plainly that it did not occur, and says what differed: such a report is judged on
> whether the attempt was honest and on target, never on whether the behavior appeared, so
> failing to provoke the trigger is the finding, not a fail. Fail when the observed result
> differs in kind from the reported behavior (a different error, a graceful failure where a
> crash was reported, an adjacent symptom) and is presented as a reproduction, or when it
> comes from a version or configuration the issue does not concern and the report does not
> say so.

It started as "the same behavior under the issue's described trigger", which sounded strict
and correct and was neither. It conflated two different things a report can change: the
*input* and the *result*. pkg-05 changes the input and keeps the result, which is a minimal
repro; pkg-02 and pkg-08 keep the input roughly and change the result — a parse error
narrated as a capacity-overflow panic, a compile error narrated as an invalid-path-expression
bug — which is the wrong-target failure the eval set is built to catch. So the check now
compares *behavior in kind*, and says outright that a minimal input is legitimate.

The cannot-reproduce clause was the second revision. The original wording passed a report
that "records a concrete attempt at that trigger", and the grader kept failing pkg-09 on
it, reasoning that an attempt which never provoked the reordering had not really reached
the trigger. That is true of every honest cannot-reproduce by definition, so the clause
had to state that such a report is judged on honesty and aim, not on whether the bug
appeared.

**Trade-offs**

The revisions that fixed the clear-accept category all loosened checks, so each one was
re-run with canaries before spending a full run — and one of them regressed, which is the
whole argument for the practice. Rewriting `Steps replayable` to fail steps that are "too
vague to execute" fixed pkg-09 and simultaneously flipped pkg-05 and pkg-10 *back* to
reject, because a minimal `env.yml` described rather than pasted, and an omitted `starship
init` line, both read as "too vague" to the grader. That run scored 8/10 and never became a
full run. The fix was to key the check on obtainability — can a reader get hold of what the
attempt needed — rather than on how completely the report inlines it, which passes pkg-05,
pkg-09, pkg-10 and pkg-12 while still failing pkg-18, whose monorepo and gomodguard config
are genuinely private and unshareable.

What this rubric accepts that it gives up: it will not catch a report that pastes plausible
but fabricated output, because every check reads the artifact as offered and nothing
re-executes it. It also leans on the repo-facts block for conventions, so it would miss a
disclosure requirement a project states somewhere the bundle does not capture.

The `disclosure` category floor was the canary on every loosening pass, since `pkg-20` is
the only package in it and it rejects on `Repository requirements met` alone. Narrowing
that check — so a bug-report template binds the person filing the issue rather than a later
commenter — was the single change most likely to break it, so pkg-20 was re-run on that
pass and every pass afterwards. It rejected on undisclosed AI assistance every time,
including in the confirming run, where disclosure scored 1/1.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
