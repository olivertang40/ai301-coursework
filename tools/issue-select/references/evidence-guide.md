# Evidence Guide

This guide maps each check family to the exact surfaces where its evidence lives on GitHub.
For every check, record one concrete fact — a date, a count, a name, or a label — never an adjective.

---

## Family 1 · Community alive

**Question:** Is there a maintainer who still merges and replies?

### commits-alive

Where to look:
- Repository main page → commits link (e.g., `github.com/owner/repo/commits/main`)
- Look at the last 5 commits: author name, date, whether it is a merge commit.

What counts:
- A commit authored or merged by someone with write access (not a bot, not a first-time contributor's commit that was never merged).
- A merge commit counts because a maintainer triggered it.

Record: the date of the most recent human merge commit.

### responds-to-issues

Where to look:
- The repository's Issues tab, sorted by "Recently updated".
- Open the last 5 updated issues and look for a reply from a repository member or owner (blue "Member" or "Owner" badge next to the username).

What counts:
- A substantive reply (not just a bot label or auto-close message).
- The date of that reply.

Record: the date of the most recent maintainer reply, and the issue number it appeared in.

---

## Family 2 · Repo in use

**Question:** Does this project still ship releases and have real users?

### shipped-recently

Where to look:
- Repository main page → right sidebar → "Releases" section, or
- `github.com/owner/repo/releases`

What counts:
- The date of the most recent published release (pre-releases count if no stable release exists).
- A release that predates the threshold in the rubric is a fail.

Record: version tag and publish date of the latest release.

### has-users

Where to look:
- Repository main page → star count, fork count, and "Used by" count (right sidebar).
- npm/PyPI/crates.io page if the project publishes a package (check README for install instructions).

What counts:
- Star count above the rubric threshold, OR
- A package with active download numbers (check the package registry).

Record: star count and fork count, or download count if a package registry was checked.

---

## Family 3 · Scope fits contributor

**Question:** Is this a single bounded change that a new contributor can finish?

### scope-bounded

Where to look:
- The issue body itself: is there a clear description of one specific change?
- Labels: `good first issue`, `help wanted`, `bug`, `documentation`.
- Any linked specification, design doc, or "acceptance criteria" in the issue.

What counts as bounded:
- One file or one function to change, clearly identified.
- A bug with a reproduction case.
- A documentation fix with a specific file/section named.

What fails:
- "Refactor the whole X module."
- "Add support for Y" with no specification of what Y means.
- Multiple unrelated tasks listed in one issue.

Record: quote the one-line summary of the change from the issue title or body.

### spec-present

Where to look:
- Issue body: reproduction steps, expected vs. actual behavior, or a concrete specification of the desired outcome.
- Linked design docs, screenshots, or error messages.

What counts:
- A bug: reproduction steps + expected behavior + actual behavior.
- A feature: a concrete description of the desired output or behavior change.
- A documentation fix: the exact section or wording to change.

What fails:
- "This is broken, please fix." (no reproduction steps)
- "We should improve X." (no concrete specification)

Record: quote the specific reproduction step or acceptance criterion from the issue body.

---

## Family 4 · Issue is unclaimed

**Question:** Is the issue available to take?

### no-assignee

Where to look:
- Issue page right sidebar → "Assignees" section.

What counts as unclaimed:
- No assignee listed, OR
- The only assignee is a bot (e.g., `github-actions[bot]`).

Record: "No assignee" or the assignee's username if one exists.

### no-open-pr

Where to look:
- Issue page → "Development" sidebar section (linked PRs appear here), OR
- Pull Requests tab filtered by the issue number: search `is:pr is:open linked:issue-N`.

What counts:
- No open PR linked to this issue, OR
- The only linked PR is closed/merged.
- For the course sandbox repo: a linked PR opened more than 14 days ago by a classmate
  does not block you (see scope.md).

Record: "No linked open PR" or the PR number and its open date.

### no-fresh-claim

Where to look:
- Issue comments, sorted oldest to newest.
- Look for comments containing "I'll take this", "I'd like to work on this", "assigning myself", or similar within the last 14 days.

What counts as unclaimed:
- No such comment in the last 14 days, OR
- Comment exists but was posted more than 14 days ago.

Record: "No claim comment in last 14 days" or the date and text of the most recent claim comment.
