# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Environment recorded | The repro report's environment record, compared with the operating system, version, and other target details named in the issue and repo-facts block. | Pass if the report identifies the relevant system and application/version details needed to interpret the attempt, and explicitly notes any material difference from the issue's target. A missing or materially ambiguous environment fails. | required |
| Steps replayable | The setup and action sequence behind the attempt that produced the report's artifact, read against the issue's trigger. | Pass if a reader could obtain or recreate what the attempt needs and run it: the commands or actions are concrete, and each input is given, quoted, described closely enough to rebuild, or available from the issue or the public project. Routine setup the tool's own docs cover, a file or script the report characterises rather than pastes, and a further variation mentioned without its own artifact are all obtainable, and none of them fail this check. Fail only when an input is private, unshared, or otherwise unavailable to the reader, or when the actions are left so unspecified that there is nothing to run. Whether the trigger fired belongs to the Correct issue behavior check. | required |
| Correct issue behavior | The issue's described symptom and trigger compared with the report's observed result and artifacts. | Pass if the artifact shows the behavior the issue describes. A simplified or minimal input that still produces that behavior is a legitimate reproduction, not a deviation. Also pass a cannot-reproduce report whose attempt was aimed at the issue's behavior, states plainly that it did not occur, and says what differed: such a report is judged on whether the attempt was honest and on target, never on whether the behavior appeared, so failing to provoke the trigger is the finding, not a fail. Fail when the observed result differs in kind from the reported behavior (a different error, a graceful failure where a crash was reported, an adjacent symptom) and is presented as a reproduction, or when it comes from a version or configuration the issue does not concern and the report does not say so. | required |
| Outcome has evidence | The repro report's quoted output, logs, screenshots, or other directly described observations, checked against its stated result. | Pass if the report provides an observable result from the attempt that supports either reproduction or an inability to reproduce. A bare assertion, conclusion, or claim that something happens without an observed result fails. | required |
| Claims stay within evidence | The claim comment and repro report, especially statements about frequency, affected users or systems, cause, severity, and what the author will deliver, compared with the evidence in the package. | Pass if each factual claim is supported by the issue context or the author's reported attempt, and the report distinguishes observation from hypothesis. A claim to have reproduced the issue is supported when the author's own artifact shows that behavior, including through a minimal input. Judge assertions of fact and promises, not opinions: a statement about how the tool ought to behave, or a restatement of the fix the issue itself asks for, is a stated expectation and is not weighed here. Unsupported generalizations, asserted causes, certainty beyond the evidence, and promised outcomes or deadlines fail. | required |
| Repository requirements met | The repo-facts block's contribution and AI-use policy, compared with the claim comment and repro report. | Pass if the comments satisfy every policy the repo states for participating in an issue thread. Where the stated policy requires disclosing AI assistance, fail when no disclosure appears (treat the package as AI-assisted work); where it requires the contributor's own words, pass a comment written in a specific human voice. Judge only the repo's stated policy: a bug-report template binds the person filing the issue, so do not fail a follow-up comment for omitting template fields, and never invent a requirement the repo facts do not state. | required |
| Communication is useful | The claim comment and repro report read in the issue-thread context, including the issue's requested information and repo conventions. | Pass if the comments are relevant to this issue, state the author's contribution or observation plainly, and give maintainers concrete information to assess or act on. Irrelevant boilerplate, unsupported demands, or wording that obscures the actual observation fails. | required |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->
Accept only when every required check passes. A fail or unclear on any
required check means reject; preferred checks never change the verdict.
An honest cannot-reproduce report can pass the behavior and evidence
checks when it records the attempted trigger and the observed result.
