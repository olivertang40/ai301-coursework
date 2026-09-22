# Rubric: is this a good first issue?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| repo-active | The last 5 default-branch commit dates and the latest release in Repo facts | At least one default-branch commit or published release is within 180 days of the snapshot capture date. | required |
| not-archived | The `archived:` field in Repo facts | The repository is not archived. | required |
| maintainer-response | The five-issue maintainer first-response sample in Repo facts | At least one Owner, Member, or Collaborator response was posted within 90 days of the issue opening date. | preferred |
| visible-adoption | The repository star count in Repo facts | The repository has at least 50 stars. | preferred |
| bounded-change | The issue title, body, labels, and comments | The issue requests one coherent bug fix, documentation outcome, or behavior change; supporting edits or alternative implementation suggestions are allowed when they serve that one outcome. It fails only for an umbrella/tracking issue, support question, unresolved design debate, or unrelated work items. | required |
| workable-spec | The issue body and any linked or quoted acceptance criteria | A bug states an observable failure or reproduction; a documentation task names the intended file, section, or outcome; or a feature states a concrete desired behavior. A terse bug filed by a Member, Owner, or Collaborator with a named behavior also passes. | required |
| no-stale-attempts | The issue age, comments, and linked PRs | An issue older than 365 days passes only if it does not show repeated abandoned claims or two or more closed, unmerged implementation attempts. | required |
| ai-policy-compatible | The contribution-policy field in Repo facts | The policy is absent, permits AI-assisted contributions, or gives conditions such as disclosure, testing, or human review; it does not prohibit AI-generated code or documentation. | required |
| unassigned | The issue assignees in Repo facts | No human assignee is listed. | required |
| no-active-pr | Linked PRs in Repo facts and PRs mentioned in the issue comments | No open linked pull request exists for the issue. | required |
| no-recent-claim | The issue comments and their dates | No commenter says they will work on the issue within 14 days of the snapshot capture date. | preferred |

## Verdict rule

Accept an issue only when every `required` check passes. A `fail` or `unclear`
result on a required check rejects the issue. `preferred` checks never change
the accept/reject verdict; among accepted issues, more preferred passes rank
higher.
