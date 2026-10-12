# Search strategy: where your scout looks, and why

Each query below traces to a sentence in the fit profile in `scope.md`.
Breadth is the point of the search stage: the ranking filters do the
narrowing, so do not tighten these queries to compensate.

## Queries

From: "I am particularly interested in Python, AI/ML, developer tools, and backend software."

```bash
gh search issues "machine learning" --language Python --state open --limit 100 \
  --json title,repository,labels,assignees,author,commentsCount,createdAt,updatedAt,url
```

From: "I have worked on AI and software projects, including Python-based machine learning, computer vision, and backend development."

```bash
gh search issues "computer vision" --language Python --state open --limit 100 \
  --json title,repository,labels,assignees,author,commentsCount,createdAt,updatedAt,url
```

From: "I want to contribute to existing open-source codebases through well-scoped debugging, testing, bug fixes, and focused improvements."

```bash
gh search issues "API bug" --language Python --state open --limit 100 \
  --json title,repository,labels,assignees,author,commentsCount,createdAt,updatedAt,url
```

Run all three, combine the results, and drop duplicates by `url` before
ranking.

## Ranking filters

Apply these four steps in order. Every step uses only fields the queries
above already return — no fetching issue pages, no reading threads, no
model judgment. If a filter would need evidence the result fields do not
carry, it belongs in `rubric.md`, not here.

### 1. Exclude issues with assignees

Drop any result with one or more assignees. An assignee indicates that
someone else may already have taken responsibility for the issue.

### 2. Exclude bot-authored issues

Drop any result where either signal holds:

- `author.type` is `Bot`, or
- `author.login` ends with `[bot]`.

An auto-generated issue is never a first contribution, so it should
never consume a grading slot. Both signals above are unambiguous
statements of account identity, which is why they are safe to apply at
this stage, where nothing can be corroborated.

**Do not rely on `author.is_bot`.** In `gh search issues` output that
field is unreliable: `github-actions[bot]` is returned with
`"is_bot": false` alongside `"type": "Bot"`. Note also that
`gh issue view` reports a different shape for the same account
(`login: "app/github-actions"`, `is_bot: true`), so a filter written
against one command's shape will not hold for the other. The two
signals above are the ones that work on search results.

**Do not extend this step to login substrings.** A `User`-typed account
whose login merely contains `bot`, `bug`, `ci`, or `auto` is *not*
dropped here. Some such accounts are automation (a role account filing
generated form reports); others are ordinary contributors whose
usernames happen to contain those letters, and ranking cannot tell them
apart, because distinguishing them needs the issue body, the author's
other issues, or that account's commits — none of which this stage may
fetch. Automation that presents as a `User` is therefore caught one
stage later, by the rubric's `automated_issue_source` check, which
requires a corroborating signal before rejecting and grades genuinely
ambiguous cases `unclear` for manual review.

### 3. Sort

Sort the surviving results by:

1. `updatedAt`, descending (most recently updated first), then
2. `commentsCount`, ascending (fewer comments first), then
3. `createdAt`, descending (newer issue first), then
4. `url`, ascending (lexicographic), which makes the order fully
   deterministic.

**`commentsCount` is an advisory tie-breaker, not evidence.** A search
result's `commentsCount` can disagree with the issue itself — one has
been observed reporting `1` for an issue whose comments endpoint
returned none. It stays in the sort because this stage may use only
fields the search returned and the value is usually right, but two
limits apply. First, it never decides a verdict: the rubric's
`no_active_claim` check must read the comment thread directly and may
not substitute this number. Second, when results tie on `updatedAt` and
their `commentsCount` values are equal or look suspect, keys 3 and 4
settle the order instead — `createdAt` and `url` come from the same
search payload and are stable, so the ranking stays reproducible without
depending on a count that may be stale.

### 4. Cap at two per repository

Walk the sorted list from the top and select candidates one at a time,
keeping a running count per `repository.nameWithOwner`. Keep a result
only if fewer than two results from that same repository have already
been kept; otherwise skip it and continue down the list. Stop once five
candidates have been selected.

This preserves the sort order from step 3 — skipped results are never
reordered, the next distinct candidate simply moves up — and stops one
high-volume repository from monopolising the graded set.

## How many to grade

Grade the top **5** ranked results per scan.
