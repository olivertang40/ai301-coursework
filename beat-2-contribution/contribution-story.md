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
**Pull Request:** [GitHub PR link, once opened]

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

I installed the voice guard as a global `PreToolUse` hook in `~/.claude/settings.json`, so Claude Code runs `check_voice.py` before Bash commands, and verified the hook stops a body-less `gh issue comment --help` call while manual checks log pass/stop results. It stopped an early claim draft because I asked a question without enough supporting evidence; I revised the comment with what I had checked, then the manual check and guarded post both passed. I distilled AUCTOR's contribution rules, linting context, and test command into a 25-line `CLAUDE.local.md` and added it to `.git/info/exclude`, which `git status` confirms keeps it out of the fork diff. The template's `@AGENTS.md` import was unnecessary because the repository's root `CLAUDE.md` and `AGENTS.md` are empty, so I removed the scaffolding and kept only issue-specific notes.

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

My Oct. 27 Python-focused scout scan surfaced AUCTOR issue #25, “Add flake8 or pylint configuration,” and graded it **accept**. Its difficulty note was **ambitious**: the requested deliverable is one linter configuration, but the issue leaves the Flake8-versus-Pylint choice and the rule baseline open. This fits my profile's interest in Python configuration and developer-quality work, and I want to learn how to propose a useful, minimal lint baseline from an existing codebase without imposing rules the maintainer does not want. I checked the repository's contribution guide: it asks contributors to fork, use a feature branch, add tests for new functionality, run `pytest`, and submit a PR; it emphasizes minimalism, security review for protocol changes, and independent verification, with no AI-use policy stated.

The scout helped me find a specific, verifiable configuration gap and called out the design question I should ask before choosing a tool. It is not a substitute for checking live repository state: an earlier regrade accepted `imgproxykit#34` after its issue had closed and its PR had merged, because the rubric lacked an open-issue check. I recorded that gap and now verify issue status directly; for #25, the live issue was open and unassigned, and there was no other claim. My claim comment is [here](https://github.com/bleedZzzz/auctor/issues/25#issuecomment-6462735667).

**Toolkit**

- Tool: issue-scout; I used its four Python issue queries, ranking filters, and rubric to scan candidates and grade the live issue.
- What it produced: An `accept` verdict for AUCTOR #25, with an ambitious difficulty note identifying the undecided linter and baseline.
- Difficulties: The scout can miss issue lifecycle changes and its scan showed weak community-response/adoption evidence; earlier it accepted a closed issue.
- What changed: I added the repeated-title/same-author filter and replaced `bounded-change` with `scope-feasible`; until the rubric checks open state, I verify that directly before choosing.

---

## Understanding the Issue

**Problem Description**

[In your own words, what is broken or missing?]

**Expected Behavior**

[What should happen?]

**Current Behavior**

[What actually happens?]

**Affected Components**

[Which parts of the codebase are involved?]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Reproduction Process

**Environment Setup**

I used Microsoft Windows 11 Home 64-bit (version 10.0.26300), CPython 3.11.9, and the AUCTOR fork at upstream commit `ac71b0bee8b791867b7180b159585cf03eaf2c29`. The project supports Python 3.10 or newer. From the clone root, I created an isolated environment and installed the editable project and pytest with `python -m venv .venv` and `.\.venv\Scripts\python.exe -m pip install -e . pytest`. The initial plain `pytest` attempt could not import `auctor` because the project had not been installed; installing it in the virtual environment resolved that setup issue.

**Steps to Reproduce**

1. In the clean clone at the commit above, search tracked files for linter configuration:

   ```powershell
   $matches = git ls-files | Where-Object {
     $_ -match '(^|/)(\.flake8|\.pylintrc|pylintrc|setup\.cfg|tox\.ini)$'
   }
   if ($matches) { $matches } else {
     "No tracked Flake8/Pylint configuration, setup.cfg, or tox.ini found"
   }
   ```

2. Read the tool sections in `pyproject.toml` and check for tracked CI files:

   ```powershell
   .\.venv\Scripts\python.exe -c "import tomllib; p=tomllib.load(open('pyproject.toml','rb')); print('tool sections:', ', '.join(sorted(p.get('tool',{}))) or '(none)'); print('pytest options:', p.get('tool',{}).get('pytest',{}).get('ini_options',{}))"
   git ls-files .github
   ```

   The only tool section is pytest (`testpaths = ["tests"]`), and the `.github` search returns no paths.
3. Run `.\.venv\Scripts\python.exe -m pytest -q`; the suite completes with `3 passed`.

**Reproduction Evidence**

- **Commit showing reproduction:** none; I made no commit in the project fork.
- **Screenshots/logs:** No screenshot. The configuration search returned no matches; parsing `pyproject.toml` printed `tool sections: pytest` and `pytest options: {'testpaths': ['tests']}`; `git ls-files .github` printed no paths; pytest reported `3 passed in 1.84s`.
- **My findings:** At the checked commit, I confirmed the requested linter configuration is absent. The existing test suite passes after installing the project in an isolated environment. I did not add a linter or choose Flake8 versus Pylint; I asked the maintainer which direction and minimal baseline they prefer.

**Toolkit**

- Tool: repro-check, which graded the claim and reproduction report together against the live issue, plus PowerShell/Git and pytest for direct evidence.
- What it produced: An `accept` verdict with all seven required checks passing.
- Difficulties: The first check run could not read skill files outside its granted paths; the next run caught an unsupported CI claim because I had not yet recorded the workflow-file check.
- What changed: I recorded the exact Windows version, added `git ls-files .github` and its empty result, and reran the checker with explicit read access; it then accepted the package.

---

## Solution Approach

**Analysis**

[Your analysis of the root cause: what is causing the issue, traced
to the files and functions involved.]

**Proposed Solution**

[High-level description of your fix approach, and what you are
deliberately NOT changing.]

**Implementation Plan**

1. [Modify file X to do Y]
2. [Add or change Z]
3. [Update tests]

[Record deviations here as they happen: what changed mid-build and
why. A recorded deviation is honest work; silent drift is not.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Testing Strategy

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**[Date]**

[Entry]

**[Date]**

[Entry]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]
