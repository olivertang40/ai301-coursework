# Adding a Flake8 baseline to AUCTOR, and fixing the issue scout that found it

## Overview

AUCTOR is a small open-source Python project. Its issue [#25](https://github.com/bleedZzzz/auctor/issues/25) pointed out that the repository had no linter configuration, so contributors had no agreed style tool or settings. I found the issue with an issue scout, a Claude Code skill I set up this term. I wrote its Python fit profile, its four search queries, its ranking filters, and the grading rubric it applies to each candidate. I asked the maintainer which linter to use, then opened [PR #33](https://github.com/bleedZzzz/auctor/pull/33), which adds a minimal `.flake8` file. The maintainer reviewed it and suggested one change. I made that change, and the PR was merged on 2026-10-29. Along the way the scout failed twice: it accepted a spam issue, and later it accepted an issue that was already closed. I changed its filters and its rubric after each failure.

## What happened

### Finding the issue (and fixing the scout first)

My first scan on 2026-10-21 pulled 400 search results and left 331 eligible after filtering. I graded the top five. One of the two accepts was `xiangmaster/colin#1`. Its author had posted the same issue title in seven different repositories, so it was a batch post, not a real request from a maintainer. The rubric couldn't see this because the scan didn't record who wrote each issue. I added the author to the scan data, plus a filter that drops any issue whose author posted the same title in more than one repository. Then I checked that `gh search issues` actually returns author names. The rerun on 2026-10-27 kept 340 of 400 results.

Regrading exposed a second gap. The rubric accepted `imgproxykit#34` even though that issue was already closed and its fix had been merged. Here is the criterion it passed, as committed in my Unit 1 rubric (`tools/issue-select/rubric.md`):

```text
| bounded-change | The issue title, body, labels, and comments | The issue requests one
coherent bug fix, documentation outcome, or behavior change ... It fails only for an
umbrella/tracking issue, support question, unresolved design debate, or unrelated work
items. | required |
```

Nothing in that row asks whether the work is still open to do. I replaced `bounded-change` with `scope-feasible`, which asks whether the change can actually be done from the issue's current state. I also started checking issue status myself before choosing. The scout then accepted AUCTOR #25 with an "ambitious" difficulty note, because the issue left both the choice of linter and the rule baseline open.

### Asking before building

Rather than guess between Flake8 and Pylint, I put the question in my claim comment:

> I checked `pyproject.toml` and the tracked files: the project configures pytest but has no Flake8/Pylint config or tracked CI workflow. After installing the project in a virtual environment, `pytest -q` passes (3 passed). ... Would you prefer Flake8 or Pylint for this minimal configuration?

The maintainer replied: *"Let's go with **Flake8** to keep things lightweight and simple. A minimal .flake8 with standard settings sounds great."*

### The first version, and a scope decision

My first commit set an 88-character line limit and kept Flake8's default checks. Running it showed the existing code already had 34 findings:

```text
> python -m pytest -q                              -> 3 passed
> python -m flake8 src tests --statistics --count  -> 34 (blank-line, long-line,
                                                      bare-except, unused-import)
```

Fixing those 34 findings would have touched many source and test files that the issue never mentioned. I kept the PR to configuration only, and I said in the PR description that it "does not claim the existing codebase is lint-clean."

### Review feedback changed the fix

The maintainer tested the PR locally and wrote:

> - `flake8 src tests` correctly picks up the configuration and reports the 34 preexisting findings.
> - Keeping this PR configuration-only was the right call to keep things clean.
>
> *(Optional suggestion)*: Would you mind adding `extend-exclude = .venv,venv` under `[flake8]` so running `flake8` at root doesn't traverse local virtual environments?

My first version only worked well when you named the folders to check. If you ran `flake8 .` from the project root, it would also scan every installed library inside a local virtual environment. I added the exclusion in commit `e450761`. I reran `flake8 .` from the root, confirmed it skipped `.venv` and `venv` and still reported the same 34 findings, and reran `pytest -q` (3 passed). The final diff:

```diff
+[flake8]
+max-line-length = 88
+extend-exclude = .venv,venv
```

### Result

The maintainer replied: *"Verified locally and everything checks out. Merging now!"* PR #33 was merged on 2026-10-29 and closed issue #25. AUCTOR now has a shared Flake8 configuration that any contributor can run from the repository root.

## Limitations and what's next

**The codebase isn't lint-clean.** The configuration loads, but the code still has 34 findings, and no CI workflow runs Flake8. For now the linter is a tool contributors can choose to run. It doesn't block anything yet. Next, I would propose a follow-up issue that fixes those findings one category at a time, starting with the unused imports and bare `except` clauses, and then adds a small GitHub Actions job so the baseline stays clean.

**The scout still trusts stale data.** The `scope-feasible` change helps, but the scout still doesn't fetch the issue's current open or closed state when it grades. I check that by hand, and a manual step is easy to skip. Next, I would add a live `gh issue view --json state` check as a required rubric row, so a closed issue fails automatically.

**Some of my tool evidence is missing.** The revised scout files and the ship-gate manifest were not saved in my course repo, so the before/after comparison above relies on my dated notes for the "after" side. The PR monitor I used later also reported `NO PR YET` because the fork branch had been deleted after the merge. Next time I will commit each tool revision to the course repo when I make it, and run the monitor before deleting a merged branch.
