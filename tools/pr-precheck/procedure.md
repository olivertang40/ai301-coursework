# Procedure: how this tool grades a PR package

<!--
THIS IS THE PART YOU WRITE (second week running for the procedure).
Week 3 you wrote these steps for a plan package; this week the graded
object is a PR package, and the read that matters most is a
side-by-side: the diff against the plan, the evidence against the test
plan, the description against both. Your week-3 procedure is the
pattern; do not paste it unchanged, because its read order was built
for a different object.

Your rotation is the design brief again, and this week friction routes
three ways: a stall on WHAT to decide is a rubric gap, a stall on
WHERE to look is a procedure gap (this file), and a stall on what the
tool even reads or outputs is a frame gap (your SKILL.md). A complete
procedure lets someone who has never seen a PR package before grade
one exactly the way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
plan's scope pair before opening the diff, and list the files the plan
names" is a step; "understand the change" is a wish.
-->

## Read order

1. In live mode, read `scope.md` first. Stop if its repo line is
   unfilled or the target repo is out of scope. In eval mode, do not
   read `scope.md`.
2. Confirm that this is one package and that `rubric.md` and
   `procedure.md` contain authored content. Refuse to grade if either
   is empty or only a template.
3. Read the issue and its thread (live) or the frozen issue and thread
   (eval). Record the issue's requested outcome, relevant maintainer
   direction, and issue identifier.
4. Read the repo PR template and `docs/CONTRIBUTING.md` (live), or
   the repo-facts section (eval). Record applicable template fields,
   required checks, branch/issue rules, disclosure rules, and any
   stated contribution policy.
5. Read the plan before the candidate PR. Record its scope, named
   files, exclusions, expected behavior, test plan, and deviation
   notes. For a house-chain package, use the house plan and repro pack.
6. Read the PR title and description, then the commit list and entire
   diff (`git diff main...HEAD` in live mode), then all test evidence.
   Keep claimed behavior separate from behavior visible in the diff;
   this ordering makes later comparisons explicit.
7. In live mode, read `voice-guide.md` and note rules relevant to the
   title and description. Do not apply it in eval mode.

## Evidence gathering

Use `references/evidence-guide.md` to locate each item. Build four
short evidence sets before grading:

- **Plan fidelity:** list planned files and behavior beside changed
  files and behavior; map each mismatch to a specific deviation note
  or mark it unexplained. Match material title/description claims to
  the corresponding diff and plan evidence.
- **Test evidence:** pair each planned test/repro and expected result
  with its actual command or step, captured output, and reported
  result. Separately list repository checks required by the template
  or policy and their outcomes. Record an honest failure or
  no-tests-run result as evidence, not as a successful test.
- **Diff quality:** identify the hunks that implement the plan and
  any unrelated files/hunks, debug or generated debris, dead or
  commented-out code, or churn that obscures the behavior. Use the
  commit list only to locate changes, not as a quality proxy.
- **Standards and communication:** map each applicable template
  request and policy requirement to the actual title, description,
  evidence, branch, or issue-thread response. Mark requirements not
  present in the repo facts as not applicable; never infer a policy.

## Check execution

Run every rubric check in its listed order using only the gathered
evidence and that check's pass condition. For each one, choose `pass`,
`fail`, or `unclear` and cite the decisive fact or quote in one
evidence line. Missing evidence is `unclear`, not an assumed pass;
report the exact missing input. Do not infer that an unmentioned test
passed, that an unmentioned change was intended, or that a policy
exists when the package/repository does not state one. A transparent
test failure counts as test evidence but is not a pass where the
repository explicitly requires success. In live mode, separately
report voice-guide violations; they do not change a check grade unless
the rubric independently covers the same fact. Do not reread or
re-grade unrelated evidence once a check's mapped facts are recorded.

<!-- How one check runs against gathered evidence: in what order the
checks execute, what an executor does when evidence for a check is
genuinely absent, and when a check may be graded without re-reading
the whole package. A complete procedure makes two executors grade the
same package the same way. -->

## Verdict assembly

Apply the rubric's verdict rule exactly: return `accept` only if every
required check passes; otherwise return `reject`, with `unclear`
counting as a required-check failure. Include all check results in
rubric order. In the readable summary, identify the first failing or
unclear required check in rubric order as the decisive reason and cite
its evidence; mention any other required failures without replacing
that deciding evidence. End with the contract's exact fenced JSON
schema, valid and last, using the PR URL or bundle id as `item`. Never
emit a third verdict or put text after the JSON block.

<!-- How the per-check grades become the final accept or reject:
apply your rubric's verdict rule, state how unclear grades enter it,
and say what gets quoted in the output for the deciding check: the
check whose failure the verdict turned on. When more than one check
failed, your procedure picks which one gets quoted (first failing
required check in rubric order is a fine rule); nothing picks it for
you, so write the rule down. A complete procedure produces the same
verdict from the same grades, every time. -->
