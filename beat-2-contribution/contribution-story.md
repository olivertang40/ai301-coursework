# Contribution: Add flake8 or pylint configuration

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** [1]
**Student:** Oliver Tang
**GitHub Username:** olivertang40
**Issue:** https://github.com/bleedZzzz/auctor/issues/25
**Pull Request:** https://github.com/bleedZzzz/auctor/pull/33

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: Built and ran a Python-focused issue scout**

I installed the Unit 5 scout over my Unit 1 skill, kept its rubric and evidence guide, and wrote a Python fit profile with four 100-result title queries and top-five ranking filters. The Oct. 21 scan left 331 of 400 results eligible; its five grades (two accepted, three rejected) exposed a blind spot when it accepted `xiangmaster/colin#1`, whose author had posted the same issue title across seven repositories. I added author data and a deterministic same-title, multi-repository exclusion, verified that `gh search issues` returns author names, and reran the scan on Oct. 27; 340 of 400 results remained after the assigned, stale, and duplicate-batch filters, although the Claude CLI attempt was blocked by permissions, so I gathered the results directly with read-only `gh` commands. Regrading also showed that the rubric could accept an issue that was already closed and merged, so I replaced `bounded-change` with `scope-feasible` and noted that I must still verify an issue is open before choosing it.

**Unit 6: Installed the voice guard and wrote a local AUCTOR repo memory**

I used the installed voice guard to check my claim draft; it stopped an early version for not grounding the question in enough specific evidence, and the revised draft passed. I copied the memory template into my AUCTOR fork, distilled its contribution rules, linting context, and test commands into `CLAUDE.local.md`, and added that filename to `.git/info/exclude`; `git status` confirms it stays out of the fork diff. The template's scaffolding and `@AGENTS.md` import were unnecessary because the repository's root `CLAUDE.md` and `AGENTS.md` are empty, so I removed them and kept only issue-specific notes.

**Unit 7: Checked for the ship-gate evidence on my AUCTOR branch**

I searched the course repository and `C:\dev-fun` for `ship-manifest.md` and gate reports, but none were present; the monitor also confirmed that `~/.claude/ship-gate/gate-log.md` is missing. The available PR evidence shows that PR #33 was merged after `pytest -q` passed (3 tests) and Flake8 loaded the configuration, but it does not establish which checks the ship-gate itself ran. I recorded the evidence gap rather than guessing at the gate result; if I recover the manifest or report, I will replace this note with its actual outcome.

**Unit 8: Verified the PR monitor and wrote a repo-specific playbook**

I ran the monitor in my AUCTOR clone on `feature/25-flake8-config`, but it reported `NO PR YET` because the fork branch had been deleted after PR #33 merged. It drafted only a ship-gate reminder and made no Claude call; I verified the merge directly on GitHub and did not post the reminder. Setting the clone's default repository to upstream and restoring the PR head locally did not fix the lookup, so I recorded the limitation and will run the monitor before a branch is deleted next time. The five recent merged PRs received maintainer action within about a day, so I set a three-day nudge threshold.

---

## Why I Chose This Issue

My Oct. 27 Python-focused scout scan surfaced AUCTOR issue #25, “Add flake8 or pylint configuration,” and graded it **accept**. Its difficulty note was **ambitious**: the requested deliverable is one linter configuration, but the issue leaves the Flake8-versus-Pylint choice and the rule baseline open. This fits my profile's interest in Python configuration and developer-quality work, and I wanted to learn how to propose a useful, minimal lint baseline without imposing rules the maintainer did not want. I checked the repository's contribution guide: it asks contributors to fork, use a feature branch, add tests for new functionality, run `pytest`, and submit a PR; it emphasizes minimalism, security review for protocol changes, and independent verification, with no AI-use policy stated.

The scout helped me find a specific, verifiable configuration gap and called out the design question I should ask before choosing a tool. It is not a substitute for checking live repository state: an earlier regrade accepted `imgproxykit#34` after its issue had closed and its PR had merged, because the rubric lacked an open-issue check. I recorded that gap and now verify issue status directly; for #25, the live issue was open and unassigned, and there was no other claim. My claim comment is [here](https://github.com/bleedZzzz/auctor/issues/25#issuecomment-6462735667).

**Toolkit**

- Tool: issue-scout; I used its four Python issue queries, ranking filters, and rubric to scan candidates and grade the live issue.
- What it produced: An `accept` verdict for AUCTOR #25, with an ambitious difficulty note identifying the undecided linter and baseline.
- Difficulties: The scout can miss issue lifecycle changes and its scan showed weak community-response/adoption evidence; earlier it accepted a closed issue.
- What changed: I added the repeated-title/same-author filter and replaced `bounded-change` with `scope-feasible`; until the rubric checks open state, I verify that directly before choosing.

---

## Understanding the Issue

**Problem Description**

The repository had no Flake8 or Pylint configuration, so contributors had no agreed linter choice or shared baseline.

**Expected Behavior**

A minimal repository-level linter configuration should make the selected tool's settings consistent without forcing unrelated source cleanup.

**Current Behavior**

Before PR #33, the root had no `.flake8` or Pylint config; `pyproject.toml` configured pytest only. The issue also left the linter choice open.

**Affected Components**

The repository root configuration (`.flake8`) and existing test configuration in `pyproject.toml`; no application source or tests needed changes.

**Toolkit**

- Tool: GitHub issue #25, `pyproject.toml`, and tracked-file inspection; I also ran `pytest -q`.
- What it produced: Confirmed the missing linter configuration and CI workflow; the existing test suite passed (3 tests).
- Difficulties: The issue did not specify Flake8 versus Pylint or a style baseline.
- What changed: I asked the maintainer to choose; they requested a minimal Flake8 configuration.

---

## Reproduction Process

**Environment Setup**

Windows; AUCTOR declares Python 3.10 or newer in `pyproject.toml` (the exact interpreter patch version used for the original run was not recorded). I created a virtual environment, installed the project editable with `pip install -e .`, and ran the repository's pytest suite. The project README documents the editable install; `CONTRIBUTING.md` says to run `pytest`.

**Steps to Reproduce**

1. Check out the fork's base commit, [`ac71b0b`](https://github.com/olivertang40/auctor/commit/ac71b0bee8b791867b7180b159585cf03eaf2c29), from before PR #33.
2. Inspect the root for `.flake8` and Pylint configuration, and check `pyproject.toml` for linter settings.
3. Run `pytest -q`; the three tests pass, but there is no repository-level linter configuration.

**Reproduction Evidence**

- **Commit showing reproduction:** [AUCTOR base commit `ac71b0b`](https://github.com/olivertang40/auctor/commit/ac71b0bee8b791867b7180b159585cf03eaf2c29)
- **Screenshots/logs:** No screenshot; the claim and test result are recorded in [the issue thread](https://github.com/bleedZzzz/auctor/issues/25#issuecomment-6462735667).
- **My findings:** The gap was reproducible as missing repository configuration, not a runtime failure. The maintainer chose Flake8 in response to my question.

**Toolkit**

- Tool: The repro-check skill, PowerShell/Git, and pytest; I used them to check the claim and reproduction evidence against the live issue.
- What it produced: An `accept` verdict with all seven required checks passing.
- Difficulties: The first check run could not read skill files outside its granted paths; the next run caught an unsupported CI claim because I had not yet recorded the workflow-file check.
- What changed: I recorded the exact Windows version, added `git ls-files .github` and its empty result, and reran the checker with explicit read access; it then accepted the package.

---

## Solution Approach

**Analysis**

The root cause was missing repository-level lint configuration: `pyproject.toml` contained pytest settings but no Flake8/Pylint settings, and there was no tracked CI workflow. After the maintainer chose Flake8, the remaining task was to define a small, explicit baseline without turning the issue into a cleanup of 34 pre-existing findings.

**Proposed Solution**

Add `.flake8` with an 88-character line limit and Flake8's default checks, then exclude `.venv` and `venv` from root-level runs. Deliberately leave dependencies, CI, application code, and existing lint findings unchanged.

**Implementation Plan**

1. Add `.flake8` with `max-line-length = 88`.
2. Keep the default Flake8 checks and add `extend-exclude = .venv,venv` after the maintainer's suggestion.
3. Run pytest and Flake8 at the source/test paths and repository root; no test files need changes for configuration-only behavior.

**Toolkit**

- Tool: GitHub issue discussion, Git, and Flake8; I used them to confirm the maintainer's choice and keep the change to one config file.
- What it produced: A minimal `.flake8` file with the selected line limit, default checks, and virtual-environment exclusions.
- Difficulties: Flake8 reported 34 existing findings, and cleaning those up was outside the issue's scope.
- What changed: I left application and test files untouched and added the requested exclusion so root-level linting would not traverse local environments.

---

## Testing Strategy

Run `.\.venv\Scripts\python.exe -m pytest -q`; it passed with 3 tests. Run `.\.venv\Scripts\python.exe -m flake8 src tests --statistics --count`; the configuration loads and reports the 34 pre-existing findings rather than claiming a clean baseline. After adding `extend-exclude`, run `.\.venv\Scripts\python.exe -m flake8 .`; it skips `.venv` and `venv` and still reports the same 34 findings.

**Toolkit**

- Tool: pytest and Flake8 from the project's virtual environment.
- What it produced: `pytest -q` passed (3 tests); targeted and root-level Flake8 runs loaded the config, skipped local virtual environments, and reported the same 34 existing findings.
- Difficulties: The lint baseline is not clean, so the count is evidence of configuration loading rather than a passing lint gate.
- What changed: I kept the PR configuration-only and documented the pre-existing findings instead of expanding into unrelated cleanup.

---

## Implementation Notes

2026-10-21: Ran the initial Python scout scan across 400 results; 331 were eligible, and I graded five issues (two accepted and three rejected). The search surfaced the same issue title from one author across seven repositories, so I added author data and a same-title, multi-repository exclusion and verified that the query returned author names.

2026-10-27: Reran the scan with 340 of 400 results remaining after the assigned, stale, and duplicate-batch filters. The Claude CLI attempt was blocked by permissions, so I gathered results with read-only `gh` commands; regrading also exposed a closed-and-merged issue that the rubric had accepted, so I replaced `bounded-change` with `scope-feasible` and recorded that I must check issue status directly.

2026-10-28: Checked AUCTOR issue #25, verified that `pyproject.toml` had pytest settings but no linter configuration, and ran `pytest -q` (3 passed). I asked the maintainer whether to use Flake8 or Pylint; they chose Flake8 and requested a minimal standard configuration.

2026-10-29: Added `.flake8` with an 88-character limit and default checks, then opened PR #33. The maintainer suggested excluding `.venv` and `venv`; I added `extend-exclude`, reran tests and root-level Flake8, and the maintainer merged the PR.

2026-11-11: Confirmed the PR monitor was installed, wrote an AUCTOR-specific playbook, and ran the monitor on the PR branch. It returned `NO PR YET` because the fork branch had been deleted after merge; I verified the merged state directly and did not post the generated ship-gate reminder.

**Toolkit**

- Tool: Git/GitHub issue and PR history, plus the PR monitor's state and full-run report.
- What it produced: A dated record of the maintainer's choice and suggestion, the two configuration commits, test results, and merge.
- Difficulties: The monitor could not resolve the merged PR after its source branch was deleted from the fork.
- What changed: I verified the state by PR URL instead of trusting `NO PR YET`, and will run the monitor before a merged PR branch is deleted next time.

---

## Pull Request

**PR Link:** https://github.com/bleedZzzz/auctor/pull/33

**PR Description:** Added a minimal `.flake8` configuration with an 88-character line limit and Flake8's default checks. The change is configuration-only; `pytest -q` passed (3 tests), while Flake8 reported 34 pre-existing findings. The maintainer's optional suggestion to exclude local virtual environments was added before merge.

**Maintainer Feedback:**

- 2026-10-28: In the issue thread, the maintainer chose Flake8 and requested a minimal standard configuration.
- 2026-10-29: Added `.flake8` with an 88-character limit and default checks in PR #33.
- 2026-10-29: In the issue thread, the maintainer suggested excluding `.venv` and `venv` from root-level lint runs.
- 2026-10-29: Added `extend-exclude`; verified the virtual environments were skipped, the 34 pre-existing findings remained, and `pytest -q` passed (3 tests).
- 2026-10-29: The maintainer confirmed the verification and said the PR was ready to merge; PR #33 was merged without further requested changes.

**Status:** Merged

**Toolkit**

- Tool: The Unit 7 ship-gate and GitHub CLI; the gate manifest and report were unavailable, so I checked the PR's live history directly.
- What it produced: No verifiable ship-gate result; GitHub confirmed PR #33 was merged on 2026-10-29 after the maintainer verified the tests and Flake8 configuration.
- Difficulties: I could not find `ship-manifest.md` or a gate report in the course repo or `C:\dev-fun`, and the ship-gate log was absent.
- What changed: I recorded the missing evidence rather than claiming the gate passed or inventing its commands.

---

## Learnings and Reflections

**Technical Skills Gained**

I learned how Flake8 reads a root `.flake8` file, how `max-line-length` and `extend-exclude` affect local runs, and how to distinguish a loaded lint configuration from a clean codebase. I also learned to treat a tool's branch-based PR lookup as a convenience, not the source of truth after a branch is deleted.

**Challenges Overcome**

The issue left the linter choice open, and the existing code produced 34 Flake8 findings. I asked the maintainer to choose Flake8, kept the implementation to configuration, and added the requested virtual-environment exclusions without changing unrelated code.

**What I'd Do Differently Next Time**

Next time I would check that an issue is still open immediately before claiming it, because the scout previously accepted a closed issue. I would also preserve or monitor the PR branch before it is deleted so the monitor can still associate a merged PR with its branch.

---

## Resources Used

The AUCTOR contribution guide informed the fork/branch/test workflow; issue #25 clarified the missing configuration and the maintainer's preferred linter; PR #33 records the implementation, checks, and merge.

- [AUCTOR `CONTRIBUTING.md`](https://github.com/bleedZzzz/auctor/blob/main/CONTRIBUTING.md)
- [Issue #25 and maintainer discussion](https://github.com/bleedZzzz/auctor/issues/25)
- [Merged PR #33](https://github.com/bleedZzzz/auctor/pull/33)
- [`pyproject.toml`](https://github.com/bleedZzzz/auctor/blob/main/pyproject.toml)
