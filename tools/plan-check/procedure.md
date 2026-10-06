# Procedure: how this skill grades a plan package

## Read order

1. Read the repo-facts block first. Write down every requirement the
   contribution policy and AI policy state, and note for each one
   whether it applies to issue comments, to pull requests, or to "any
   form" of contribution.
2. Read the issue (title, body, labels). Write down the reported
   behavior in one line.
3. Read the thread highlights. List every comment by an OWNER, MEMBER,
   COLLABORATOR, or the maintainer who opened the issue, and every
   mention of an open or prior PR. For each, note what it decides: a
   culprit isolated, an approach proposed or rejected, a patch posted.
4. Read the repro evidence before the plan. List each numbered step,
   each artifact (output, stack trace, exit code), and each control run.
   For each control, write what it rules in or out ("same input
   without flag X works, so the tokenizer is not the cause").
5. Only now read the candidate plan, then the candidate plan comment.
   Reading the evidence first means the plan's confidence can't set
   the frame. The plan gets checked against the evidence, not the
   other way round.

## Evidence gathering

1. **Diagnosis:** copy the plan's stated cause in one sentence. Next
   to it, put the control list from read-order step 4.
2. **Scope:** list every piece of work the plan commits to (each
   approach step, each "also", each "while I'm here"). Separately,
   list what the plan explicitly defers or marks not in scope.
3. **Executability:** record the files, functions, or code sites the
   plan names, and the mechanism it chooses. Record any phrase that
   leaves the core choice open ("or", "whichever", "not sure",
   "somewhere", "investigate").
4. **Test plan:** copy the test plan's expected outcome(s). Note which
   repro step each one maps to.
5. **Honesty:** copy the risks/unknowns lines, if any.
6. **Comms:** from read-order step 3, record the maintainer direction
   and open PRs. From step 1, record the policy requirements that
   apply to comments. Then quote the parts of the plan comment that
   respond to each, or write "not addressed".
7. In live mode, gather the same facts from the GitHub issue thread
   (for maintainer comments, use the author association badge), the
   student's posted repro comment, the repo's CONTRIBUTING.md and any
   AI_POLICY.md, and the drafts (`plan.md`, `comment.md`). Grade only
   what the drafts contain and quote.

## Check execution

1. Run the checks in rubric table order: grounded-cause,
   bounded-scope, executable, decisive-test, honest-unknowns,
   thread-direction, repo-policy. Grade every check, even after a
   required one fails, so the output is complete.
2. For each check, apply its pass condition to the facts recorded
   under Evidence gathering only. Re-read the package only when a
   recorded fact is ambiguous.
3. grounded-cause: walk each control and artifact. If any one of them
   contradicts the stated cause, fail and quote it. A thread or issue
   that says the same thing as the plan doesn't override a
   contradicting control. A control the plan explains only thinly, but
   which is still consistent with the cause, is not a contradiction:
   pass.
4. bounded-scope: for each committed work item, ask "would the
   reproduced bug still be fixed and tested without this?" If yes and
   the item isn't deferred, fail and name the item. Exception: the same
   fix applied to (or an audit of) other occurrences of the same defect
   in the same function or file is part of the fix. Work that reaches
   into other components, or that is a different kind of work
   (refactor, upgrade, new option), is not.
5. executable: fail if the component/layer or the core mechanism comes
   with an open-choice phrase. A named component plus a decided
   mechanism passes even if exact function names come later. Open
   questions about secondary details don't fail it.
6. decisive-test: fail unless at least one expected outcome would
   visibly differ between the broken and fixed build for the
   reproduced case.
7. thread-direction: if there is no maintainer direction and no open
   PR, pass. Otherwise check that the comment follows each direction
   or names it and gives a reason.
8. repo-policy: for each requirement that applies to comments or "any
   form", check that the comment meets it. Treat the work as
   AI-assisted. A required disclosure that is absent is a fail.
9. Evidence genuinely absent (for example, no repro block, or no test
   plan at all): grade `unclear` and say what is missing. If the
   evidence is present but arguable, decide pass or fail by the pass
   condition and quote the deciding fact.

## Verdict assembly

1. Collect the grades of the required checks: grounded-cause,
   bounded-scope, executable, decisive-test, thread-direction,
   repo-policy.
2. Count each `unclear` as `fail`.
3. If every required grade is `pass`, the verdict is `accept`.
   Otherwise it is `reject`. honest-unknowns is reported but never
   changes the verdict.
4. In the summary, name the deciding check: the first failing required
   check in table order, with its quoted evidence. For an accept, write
   "all required checks pass".
5. Emit the JSON block last, with one entry per check (all seven), each
   with the one-line fact that decided it.
