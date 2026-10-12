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
| repo_liveness | Repo-facts block: archived flag, latest release status and date, last push to any branch, last 5 default-branch commits (each commit's author account, that account's type, and for a merge commit the account that performed the merge), and contribution-policy statement; use the capture date for recency | Pass if the repo is not archived, its last push is within 180 days of capture, the last 5 default-branch commits meet the human-activity minimum defined below the table, and either the latest release is within 12 months of capture or the bundle says no release has been published. A published release is not required. Also pass when the policy is silent, permits AI assistance, or imposes conditions that do not prohibit the contribution; fail when the bundle explicitly prohibits AI-generated code, AI-generated documentation, or AI-generated contributions of the type required by this task. | required |
| repo_venue | Issue body and complete comment thread: where the described defect actually occurs (files in this repository, a hosted website, a remote API endpoint, or a third-party service); the repository's description and README role; whether the repository holds the affected code or only collects reports about it; any statement by the reporter or a maintainer about the correct venue | Pass if the change that would resolve the issue lands in files this repository contains — its code, documentation, configuration, or data. Fail when the defect is in a separate hosted service, website, or remote API that this repository does not contain (for example a page-load failure on an external site, or a server-side API response), when the repository is an issue-collection or aggregation tracker rather than the home of the affected code, or when the reporter or a maintainer states the issue belongs elsewhere. A repository that wraps, packages, or documents an external service still passes when the requested change is to this repository's own files. Grade unclear when the evidence does not establish where a fix would land. | required |
| automated_issue_source | The issue's own author login and account type; the body's structure (machine-readable blocks, embedded JSON or user-agent dumps, auto-generated footers, fixed form templates, absence of free-form human text); whether a run of near-identical issues exists from the same author; and, when that account also commits, whether its commits are mechanically uniform | Pass if the issue was written by a person. Pass by default: an account typed `User` whose body is prose addressed to a human reader passes **even when its login contains strings such as `bot`, `bug`, `ci`, or `auto`** — a login substring is never sufficient on its own. Fail only when an automation signal in the author (`type` is `Bot`, login ends in `[bot]`, or the login names a role or automation) is corroborated by at least one independent signal: a machine-readable block or auto-generated footer in the body, a fixed form template with no free-form human text, a run of near-identical issues from the same author, or mechanically uniform commits by that account. Grade unclear when exactly one signal is present and no corroborating evidence is available either way. | required |
| bounded_scope | Issue body and complete comment thread: requested user-visible outcome, reproduction or observed-vs-expected behavior, named files or examples, labels and author association, design discussion, issue age, and history of claims or linked PRs | Pass if there is one focused bug, enhancement, documentation task, or compatibility problem; the desired user-visible result is clear; and the evidence is sufficient to determine successful completion. Multiple named files may support one coherent deliverable, and multiple technical causes or implementation approaches pass when they address the same settled outcome. Concise or informal issues pass when they contain concrete behavior, reproduction, or expected-vs-observed information; maintainer/collaborator authorship or a `good first issue` label may strengthen the evidence but is not required. A tentatively phrased suggestion ("maybe it would be useful to…", "it might be worth…") passes when it names a specific, bounded change with a determinable outcome: phrasing is not the test, the definiteness and size of the requested change is. Tentative phrasing and maintainer silence are never read as endorsement — record the missing endorsement under `maintainer_engagement` and state it in the summary. Fail for an umbrella/tracking issue, unresolved product/design/API behavior, competing requirements that leave the outcome unclear, primarily open-ended investigation without a defined outcome, a tentative suggestion that leaves the deliverable undefined, or repeated abandoned attempts plus unresolved direction demonstrating that the issue is not currently well-bounded. Do not fail merely because there are several technical approaches or possible causes, formal acceptance criteria are absent, the wording is hedged, or closed historical PRs exist. | required |
| no_active_claim | Repo-facts block and the complete comment thread read directly from the issue: current assignee state, linked PR states, and current claim or work-in-progress comments | Pass if there is no current assignee, no open linked PR, and no current comment or thread indication that someone has claimed the issue or is actively working on it. Closed PRs, stale claims, old comments, and abandoned work do not count as current claims by themselves. Read the comment thread itself; **never substitute a search result's `commentsCount`**, which is a ranking aid, can be stale, and has been observed reporting one comment on an issue with none. In live mode, confirm against the issue's comments endpoint when the thread is ambiguous. | required |
| maintainer_engagement | Comment thread: `author_association` on each comment (OWNER, MEMBER, COLLABORATOR) and the date of any maintainer comment on this issue; the issue's open date against the capture date; the maintainer first-response sample under Repo facts | Pass if a maintainer (OWNER, MEMBER, or COLLABORATOR) has responded on this issue, **or** the issue is less than 14 days old — too new for silence to carry meaning. Fail if the issue is 90 days or older and carries no maintainer response of any kind. Grade unclear between 14 and 90 days old with no maintainer response. Engagement is evidence, not proof: a maintainer comment is not acceptance, assignment, or permission, and maintainer silence is not rejection. | preferred |
| adoption_context | Repo line and repo front page: stars, forks, watchers, and the "Used by" counter; whether a package is published from the repository | Record the figures. Pass when the repository shows any external adoption signal — stars, forks, or a Used-by count above zero, or a published package. **No numeric threshold is set, deliberately.** Stars measure popularity, not health or maintenance: a single-digit-star personal project can be actively maintained and a heavily starred one abandoned, and no defensible cut-off was established from the evidence gathered so far. Adoption is therefore contextual evidence only and never gates a verdict. | preferred |

### Human-activity minimum (used by `repo_liveness`)

"Human activity" in the last 5 default-branch commits means, concretely:

- **At least 2 of the last 5 commits** show human development activity, where
  a commit qualifies if either (a) it is **authored** by an account that is not
  a bot (`type` is not `Bot` and the login does not end in `[bot]`), or (b) it
  is a **merge commit performed by a human account**.
- **A human-authored merge of a bot-authored PR does count** as human activity
  under (b) — a bot that lands a human's or a maintainer's reviewed work is a
  sign of life, not its absence.
- **A merge alone is not sufficient without examining the surrounding
  activity.** When (b) is the *only* human signal — no human-authored commit
  anywhere in the 5-commit window — the check additionally requires one
  corroborating maintainer action dated within 60 days of capture and found
  outside that commit list: a maintainer comment or review on any issue or PR,
  or a merged PR authored by a human. With that corroboration, grade pass;
  without it, grade unclear rather than pass.
- Commits that are uniformly mechanical (identical or templated messages
  produced by a scheduled job, content-ingest run, or form upload) do not
  count as human development activity even when the committing account is
  typed `User`.

## Verdict rule

The required checks are `repo_liveness`, `repo_venue`, `automated_issue_source`, `bounded_scope`, and `no_active_claim`. The preferred checks are `maintainer_engagement` and `adoption_context`.

Accept if every required check passes. Reject if any required check fails or is graded unclear. Treat unclear as fail: a first issue that cannot be verified is not a safe first issue to take.

When a required check is graded unclear, the verdict is reject **and the summary must flag the candidate as needing manual review**, naming the check and the specific evidence that was missing, so a person can review the rejection rather than have it disappear silently. This is how an uncertain automation signal, an unestablished venue, or an unconfirmed commit history reaches a human instead of being resolved by guesswork.

Preferred checks never change the verdict. Report their grades on every candidate, and use them to rank the accepted ones: prefer stronger `maintainer_engagement` first, then wider `adoption_context`. When an accepted issue has no maintainer response, say so explicitly in the summary — it is accepted, not endorsed.

This is a practical rubric based on the course's four families — maintainer/repo health, whether the repo is in use, scope fit for a newcomer, and whether someone else is already on the issue — plus two surfaces the field added: whether the fix even belongs in this repository, and whether a person wrote the issue at all. It uses only evidence actually present, and does not infer missing activity or missing comments.
