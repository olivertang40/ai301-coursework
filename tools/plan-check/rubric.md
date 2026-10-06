# Rubric: is this plan ready to post and build from?

A plan is ready when a maintainer could read the comment, agree, and
a stranger could build the fix from the plan without asking anything.
Every check reads the plan against the package's own evidence (repro
steps, controls, thread, repo facts), never against how polished it
sounds. Treat every package as AI-assisted work.

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| grounded-cause | The plan's stated cause (diagnosis line) read against every step, artifact, and control run in the repro-evidence block (see evidence guide: Diagnosis and grounding) | The stated cause explains what the repro shows AND no repro step, control, or artifact rules it out. Fail if any control shows the behavior is fine when the blamed component still runs (or still fails when it is absent), or if an artifact shows the defect already present before the blamed code runs. Fail if the plan fixes only the symptom (a workaround, docs note, or retry) while the repro or thread isolates a code cause. Adopting a cause from the issue or thread does not pass on its own: it must also survive the repro evidence. Fail only on contradiction: a control the plan explains thinly or only partly, but which does not rule the cause out, still passes. | required |
| bounded-scope | The plan's change/approach steps and its in-scope / not-in-scope lines, read against the reproduced behavior (see evidence guide: Scope) | Every piece of work the plan commits to doing is needed to fix or regression-test the reproduced behavior. Fail if the plan commits to any extra front: a refactor or rewrite of surrounding code, a dependency upgrade or migration, a new option/setting/UI, a new framework, or porting the fix to other components "while in the area", even when the core fix is correct. Work that is explicitly deferred to a follow-up or listed as not in scope does not count against it. Applying the same fix to (or auditing) other occurrences of the same defect in the same function or file is part of the fix, not an extra front. Carrying it into other components or modules is an extra front. | required |
| executable | The plan's change and approach: named files, functions, or code sites, and the chosen mechanism (see evidence guide: Executability) | A stranger could start the build today: the plan names where the change goes (a file, a function, or a named code path inside a named component, such as "the reconnect path in the server's session handling") AND commits to one mechanism. Pinning exact function names during the build is fine when the component and the mechanism are already decided. Fail if no component or layer is chosen ("somewhere", "the input stack", "not sure which layer", "library A or library B?"), or if the core decision is left open ("X or Y, whichever is easier", "profile and see"). An open question about a secondary detail (cost tuning, an extra tool to verify) does not fail this check if the core change is decided. | required |
| decisive-test | The plan's test plan read against the repro-evidence steps and expected/actual lines (see evidence guide: Test plan) | The test plan names an observable outcome that would differ between the broken and fixed build for the reproduced behavior: the repro re-run with a stated expected result (exit code, output, color, passing named test), or a named regression test of that case. Fail if the only test is generic ("run the full suite", "CI passes"), subjective ("should feel fast", "nothing else feels broken"), or names no expected result. | required |
| honest-unknowns | The plan's risks / unknowns / open-questions lines, read against what the repro evidence actually verified (see evidence guide: Honesty) | Anything the plan has not verified (untested platforms, unmeasured cost, unchecked tools, deferred variants) is stated as unverified rather than asserted as fact. A plan with no real unknowns passes. | preferred |
| thread-direction | The plan comment and plan read against the thread highlights: comments by OWNER, MEMBER, COLLABORATOR, or the issue's maintainer-author that isolate a culprit, propose or reject an approach, post a patch, or point at an open/prior PR (see evidence guide: Comms) | If the thread contains such maintainer direction or an open PR for the same fix, the comment either follows it or names it and gives a reason for differing. Fail if the comment proposes something the maintainer already rejected, or proposes a different direction (including a workaround) without acknowledging the maintainer's isolated culprit, patch, or open PR. If the thread has no such direction, pass. | required |
| repo-policy | The plan comment read against the repo-facts block's contribution policy and AI policy (see evidence guide: Comms) | Every requirement the repo states that applies to an issue comment is met. If the policy requires disclosing AI usage in any form, or in issues/comments, the comment must disclose it (the tool or that AI was used, and to what extent). If the policy requires comments in the contributor's own words, the comment must not read as boilerplate. Requirements scoped only to pull requests (for example, "state the tool in the PR") do not fail a plan comment. No stated AI policy: pass. | required |

## Verdict rule

- `accept` if every `required` check grades `pass`. Otherwise `reject`.
- `preferred` checks (honest-unknowns) never change the verdict. Report
  them in the summary only.
- `unclear` on a required check counts as `fail`. A plan that can't be
  verified from the package isn't ready to build from. Grade `unclear`
  only when the package lacks the evidence the check needs (for
  example, no repro evidence at all). If the evidence is present and
  merely arguable, apply the pass condition and commit to pass or fail.
- When more than one required check fails, the summary quotes the
  first failing check in table order as the deciding check.
