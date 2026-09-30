# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

<!-- Where the environment record lives, and what a sufficient one
looks like against the issue's stated target. -->
In an eval bundle, look in the issue section for the target operating
system, application version, and stated prerequisites; look in the
repo-facts block for required environment fields; look in the repro
report for the environment used in the attempt. In live mode, compare
the draft report's environment record with the issue body and the
repository's bug-report template or documentation. Good evidence names
the relevant system and version and calls out a meaningful difference
from the issue's target instead of implying they match.

## Steps

<!-- Where the reproduction steps live, and what makes them followable
by a stranger, starting state to trigger. -->
In an eval bundle, find the sequence in the candidate repro report and
the trigger in the issue description. In live mode, use the draft
report and the issue body. Good steps are concrete about what was run
and leave every input obtainable: given, quoted, described closely
enough to rebuild, or available from the issue or the public project.
Ask whether a reader could get hold of what the attempt needed, not
whether the report pasted it. Routine setup covered by the tool's own
docs, a file the report characterises instead of quoting, and a further
variation mentioned without its own artifact all stay obtainable. Steps
fail when an input is private, unshared, or otherwise unavailable, or
when nothing concrete is described to run. Whether the trigger fired is
read under Behavior shown, not here; steps that run correctly and
produce no bug are still replayable.

## Behavior shown

<!-- Where the artifacts live (output excerpts, logs, screenshots),
and what it means for an artifact to show the issue's behavior rather
than an adjacent one. -->
In an eval bundle, inspect output excerpts, logs, screenshots, and
other observations included in the repro report, then compare them
directly with the behavior and trigger in the issue section. In live
mode, inspect the draft's quoted or attached artifacts and the live
issue description. Good evidence exposes the relevant observed result
and shows the same symptom the issue reports. Compare the behavior, not
the input: reducing the issue's case to a minimal example that still
produces the symptom is how a good reproduction is built, while an
artifact whose result differs in kind from the report (a graceful error
where a crash was reported, a failure from an unmentioned old version)
is a wrong-target reproduction however confidently it is narrated. An
explicit, attempt-specific observation that the behavior did not occur
can support an honest cannot-reproduce result.

## Honesty

<!-- Where claims and their backing meet: how to tell a report that
says exactly what happened (including an honest cannot-reproduce) from
one that claims more than its evidence shows. -->
In an eval bundle, compare every claim in the candidate comments with
the issue context and the report's observations. In live mode, compare
the draft's wording with the issue and the author's recorded attempt.
Good reporting separates what was observed from a suspected cause,
limits claims about frequency or affected users to evidence actually
provided, and says plainly when an attempted reproduction did not
occur. Weigh assertions of fact and promises of delivery; a view about
how the tool ought to behave, or an echo of the fix the issue itself
requests, is an expectation rather than a claim, and belongs to Comms.
A hypothesis is not proof, and an observation on one setup does not
establish that all users or systems are affected. A report that names
the limits of its own attempt is doing this check's work, not
confessing a defect: saying what differed and what might be needed is
the most useful form a cannot-reproduce can take.

## Comms

<!-- Where the words meet the repo: the claim comment against the
issue, the comments against the repo's stated templates and
contribution policy (including AI-use disclosure requirements), and
what specific-and-honest looks like next to boilerplate. -->
In an eval bundle, read the candidate claim comment and repro report
alongside the issue request and repo-facts block. In live mode, check
the issue thread, the repository's contribution policy, and the draft
comments. Good communication is specific to the issue, tells
maintainers what the author observed or plans to contribute, and obeys
the policies the repo states for commenting. Read the repo facts
precisely: a bug-report template lists what the *original reporter*
must file, so its fields are not obligations on a later confirming
comment. Contribution and AI-use policies do bind every commenter.
Treat AI disclosure as required only when the repository's stated
policy requires it, and when it does, treat an undisclosed package as
failing; do not infer unstated rules. Generic enthusiasm, demands, or
boilerplate do not substitute for actionable facts.
