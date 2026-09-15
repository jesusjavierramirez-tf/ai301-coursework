# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| repo_liveness | Repo-facts block: archived flag, latest release status and date, last push to any branch, last 5 default-branch commits, and contribution-policy statement; use the capture date for recency | Pass if the repo is not archived, its last push is within 180 days of capture, the last 5 default-branch commits show human activity, and either the latest release is within 12 months of capture or the bundle says no release has been published. A published release is not required. Also pass when the policy is silent, permits AI assistance, or imposes conditions that do not prohibit the contribution; fail when the bundle explicitly prohibits AI-generated code, AI-generated documentation, or AI-generated contributions of the type required by this task. | required |
| bounded_scope | Issue body and complete comment thread: requested user-visible outcome, reproduction or observed-vs-expected behavior, named files or examples, labels and author association, design discussion, issue age, and history of claims or linked PRs | Pass if there is one focused bug, enhancement, documentation task, or compatibility problem; the desired user-visible result is clear; and the evidence is sufficient to determine successful completion. Multiple named files may support one coherent deliverable, and multiple technical causes or implementation approaches pass when they address the same settled outcome. Concise or informal issues pass when they contain concrete behavior, reproduction, or expected-vs-observed information; maintainer/collaborator authorship or a `good first issue` label may strengthen the evidence but is not required. Fail for an umbrella/tracking issue, unresolved product/design/API behavior, competing requirements that leave the outcome unclear, primarily open-ended investigation without a defined outcome, or repeated abandoned attempts plus unresolved direction demonstrating that the issue is not currently well-bounded. Do not fail merely because there are several technical approaches or possible causes, formal acceptance criteria are absent, or closed historical PRs exist. | required |
| no_active_claim | Repo-facts block and complete comment thread: current assignee state, linked PR states, and current claim or work-in-progress comments | Pass if the bundle shows no current assignee, no open linked PR, and no current comment or thread indication that someone has claimed the issue or is actively working on it. Closed PRs, stale claims, old comments, and abandoned work do not count as current claims by themselves. | required |

## Verdict rule

Accept if all three required checks pass. Reject if any required check fails. Treat unclear as fail; a first issue that cannot be verified from the snapshot is not a safe first issue to take.

This is a practical rubric based on the course's four families: maintainer/repo health, scope fit for a newcomer, and whether someone else is already on the issue. It uses only evidence present in each bundle and does not infer missing activity or missing comments.
