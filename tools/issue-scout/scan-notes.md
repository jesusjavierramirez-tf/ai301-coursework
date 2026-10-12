# Scan notes

Friction log for issue-scout live scans. Each entry is dated and
records what the field taught, not what was fixed. Patches to
`rubric.md` and `search-strategy.md` happen separately; this file is
the evidence those patches get written from.

---

## 2026-10-12 — Scan #1 (first live scan)

**Run shape.** Three strategy queries, 100 results each. 300 results
combined, 300 unique by URL (zero overlap between the three queries).
32 dropped for having an assignee. 268 survivors ranked by `updatedAt`
descending, tie-broken by fewer comments. Top 5 graded.

**Yield: 1 accept out of 5 graded**, and the single accept is weak.
Three of the five grading slots went to issues that were never
contributable by anyone.

### Search noise

- **Keyword queries match issue *text*, not issue *quality*.** All
  three queries are bare keyword searches. `"machine learning"` matched
  auto-generated job advertisements that happen to contain the phrase.
  `"API bug"` matched a server-side API bug filed in an SDK repo whose
  code cannot fix it. Nothing in the query set asks for
  `label:"good first issue"`, `label:"help wanted"`, or any other
  signal that a maintainer considers the issue available.
- **No bot-author exclusion.** Issues authored by `app/github-actions`
  and similar are structurally never a first contribution. Three of the
  top five were bot-authored. The search results already carry the
  author, so this could be filtered for free.
- **No adoption or activity floor in the queries.** A repo created
  five weeks ago with 0 stars competes on equal terms with an
  established SDK.

### Ranking problems

- **Pure recency sort rewards high-volume automation.** Sorting by
  `updatedAt` descending with no quality floor handed **3 of the top 5
  and 13 of the top 15** to a single job-scraper repo
  (`rameshtarini/mba-internship-engine`) that files hundreds of
  auto-generated issues per day. Deduplicating by URL does not help,
  because every auto-posting is a genuinely distinct URL.
- **No per-repo cap.** Nothing prevents one high-volume repo from
  monopolising the ranked list. A cap of 1–2 results per repository
  would have freed four grading slots on this scan alone.
- **Recency selects *against* maintainer validation.** The most
  recently updated issue is, by construction, the one least likely to
  have drawn a maintainer reply yet. This is exactly the weakness in
  the one accepted candidate: created hours before the scan, zero
  comments, nobody with authority having agreed to it. The tie-break
  ("prefer fewer comments") compounds the same bias rather than
  offsetting it.

### Rubric gaps

- **`repo_liveness` has no adoption floor.** A 1-star repo with a
  single committer passes identically to a 203-star SDK. The evidence
  guide lists "adoption scale" (stars, Used-by) under *is the repo in
  use?*, but the rubric never reads it. The accepted candidate sits in
  a 1-star repo and the check raised nothing.
- **`repo_liveness`'s "human activity" wording does not mention
  merges.** `coinbase/cdp-sdk` shows five consecutive
  `cdp-repo-sync[bot]` commits on the default branch. Read literally,
  the rubric fails a demonstrably live repo. Resolving it required the
  evidence guide's bot-merge rule plus a manual fetch of PR #841 to
  discover a human (`sammccord`) performed the merge. The pass
  condition should say what the evidence guide says: a bot commit that
  merges or lands a human's PR counts as human activity.
- **No check catches "wrong repo / wrong venue."** `cdp-sdk#848` is an
  API bug whose fix lives in a hosted service, not in the repository it
  was filed in. `bounded_scope` caught it, but only because the
  reporter volunteered the fact in the first line. An issue whose fix
  lives outside the repo, filed by someone less forthcoming, would pass
  every current check.
- **`bounded_scope` is lenient about unvalidated suggestions.** The
  accepted candidate's body hedges — "*maybe* it would be useful to
  note the distinction" — with no maintainer response. The rubric says
  maintainer authorship "is not required" and not to fail for absent
  acceptance criteria, so it passes as written. Graded as a pass and
  the tension noted rather than overridden, per the skill's grading
  discipline. Worth deciding deliberately whether a hedged suggestion
  nobody with authority has endorsed should clear this check.

### Tooling / PowerShell workarounds

These cost time but needed no change to the skill.

- **`gh issue view --json authorAssociation` is not a valid field.**
  The CLI rejects it and prints the valid field list.
  `authorAssociation` exists only on *comment* objects inside the
  `comments` field, not at issue level. Use the `comments` field and
  read `authorAssociation` per comment; there is no issue-level
  equivalent through `gh issue view`.
- **`gh api --jq` breaks on expressions containing spaces.** Under
  PowerShell argument passing, a `--jq` expression with spaces arrives
  split and `gh` fails with `accepts 1 arg(s), received 9`. A
  space-free expression such as `--jq 'length'` works fine. Workaround:
  skip `--jq` entirely, pipe the raw JSON into `ConvertFrom-Json`, and
  do the shaping in PowerShell.
- **`gh` is not on `PATH` in either shell.** It lives at
  `C:\Program Files\GitHub CLI\gh.exe`. Bash reports
  `gh: command not found`; PowerShell's `Get-Command gh` returns
  nothing. Every command needs
  `$env:Path += ";C:\Program Files\GitHub CLI"` first.
- **Long multi-line PowerShell pipelines are fragile inline.** Writing
  the ranking and fetch logic to `.ps1` files in the scratchpad and
  invoking them with `&` was markedly more reliable than passing long
  compound commands as a single string.
- **Counting `assignees` needs an array wrap.** `$i.assignees.Count` is
  unreliable when the field holds a single object or null; `@(...)`
  around it before `.Count` is the safe form.

### Capture-date note

All recency thresholds were measured against **2026-10-12**, the UTC
date of the newest result in the pool. The session's stated local date
was 2026-10-11; the UTC timestamps in the search results run ahead of
it. Live mode measures against today, so pick the capture date from the
data, not the session banner, and state it in the read-out.

---

## 2026-10-12 — Scan #2 (post-strategy patch)

First scan run against the patched `search-strategy.md` (bot-author
exclusion added as step 2, per-repository cap of 2 added as step 4).
`rubric.md` was unchanged from scan #1, so differences in yield are
attributable to the strategy patch alone.

**Run shape.** All three queries succeeded, 100 results each. 300
combined, 300 unique by `url` (again zero overlap between queries). 32
dropped for assignees, 99 dropped as bot-authored, 169 sorted, 0 skipped
by the per-repo cap, 5 selected.

**Yield: 2 accepts out of 5 graded**, up from 1 of 5 in scan #1. Both
accepts are defensible candidates rather than a single weak one.

### Observations

**The bot-author filter worked, and the problem was wider than scan #1
diagnosed.** It removed 99 of 268 remaining results (37%). Scan #1
attributed the flooding to one repository; in fact the removed results
came from **eight distinct repositories**, every one authored by
`github-actions[bot]` with `type: Bot` — `mba-internship-engine` (65),
`Job-Applications` (12), `fable-job-search` (7), `BigBrainTracker` (6),
`ex-od-us` (4), `mole-logistics` (2), and two singletons. All 99 would
have passed a filter written against `is_bot`, which reads `false` for
every one of them.

**Correction to a point worth not mis-recording: the filter did *not*
catch `vlabs-bug`.** That account has `author.type: "User"` and no
`[bot]` login suffix, so it survived step 2, reached grading as
candidate #4, and then failed two rubric checks. All 99 filtered results
were `type: Bot`. This is a *gap* in the filter, not a success of it —
see the role-account observation below.

**New gap: automation accounts that are not typed as `Bot`.**
`vlabs-bug` is a plain User account that files auto-generated web-form
bug reports and whose commits are uniformly "Adding an image to the
repository" (form attachment uploads). Neither `author.type == "Bot"`
nor the `[bot]` login suffix catches a role account of this kind. The
current step 2 catches GitHub Apps; it does not catch humans-in-name-only.

**The per-repository cap skipped zero candidates, so this scan did not
test it.** The bot filter removed the flooding repositories upstream,
leaving nothing for the cap to catch. The cap remains untested against
its actual target — a *human*-authored flood from one repository. Do not
read this run as validating it.

**Search `commentsCount` disagreed with the direct issue view.** For the
AWS candidate (`sample-agentcore-cloudfront-x402-payments#39`) the
search result carried `commentsCount: 1`, while both `gh issue view` and
the `/issues/39/comments` API returned zero comments. `commentsCount` is
the step 3 tie-breaker, so a stale value can misorder results. It
changed nothing this scan, because every `updatedAt` in the top five was
distinct and the tie-breaker never fired.

**The wrong-repository / wrong-venue problem appeared again, in two of
five candidates.** `cdp-sdk#848` is a hosted-API bug filed in an SDK
repository (the reporter says so outright: "Please move or close it if
there is a better venue"). `bugs-virtual-labs#20241` is a hosted-site
page-load failure filed in a tracker repository, with no such
declaration. Both were caught by `bounded_scope`, but incidentally —
neither was caught by a check aimed at venue.

**Maintainer engagement remains unmeasured.** `repo_liveness` passed
both extremes this scan: `ai-ledger#15`, opened hours before the scan
with no maintainer reply, and
`sample-agentcore-cloudfront-x402-payments#39`, open since 2026-07-26
with zero comments in roughly 2.5 months, in a repository whose last
default-branch commit (2026-05-12) predates the issue itself.

**The "human activity" threshold in `repo_liveness` is still
undefined.** This scan required interpreting it three times against
different commit mixes: `skillquarium` passed on 2 human commits out of
the last 5 (including a human merge of PR #1023); `bugs-virtual-labs`
failed on 0 of 5; `cdp-sdk` passed on 0 human *authors* out of 5 but a
human merger on PR #841. The rubric does not say how many of the five
must show human activity, nor whether a merge counts, so these were
judgment calls rather than applications of a stated rule.

**Tooling: Bash line continuations do not work in PowerShell.** The
repaired `search-strategy.md` formats each query across two lines with a
trailing `\`. That is a POSIX continuation; PowerShell uses a backtick
and treats `\` as a literal argument. Each command was joined into a
single line before running. No other tooling friction this scan — the
scratchpad `.ps1` approach and the `$env:Path` prefix for `gh` both
carried over from scan #1 without issue.

### Proposed changes (not applied)

These follow from the observations above and are recorded for a future
patch session. Nothing in this section has been implemented.

- Extend step 2 of the strategy, or add a rubric check, to catch
  automation role accounts that are typed `User`. Possible signals: a
  login containing `bug`/`bot`/`ci`, a body carrying a machine-readable
  block, or uniform mechanical commit messages. Needs care — a crude
  login substring match would catch legitimate contributors.
- Add a venue check to `rubric.md`: does the fix for this issue live in
  *this* repository? Two of five candidates failed on this in scan #2
  and one of five in scan #1.
- Give `repo_liveness` an explicit human-activity threshold, state
  whether a human merge of a bot-authored PR satisfies it, and consider
  an adoption floor (stars / Used-by), which is still unread.
- Consider a maintainer-engagement signal, bounded both ways: an issue
  too new to have drawn a reply and an issue stale for months with none
  are different problems, and `repo_liveness` currently distinguishes
  neither.
- Re-verify `commentsCount` from the issue itself before relying on it,
  or drop it as the tie-breaker.
- Decide deliberately whether a hedged suggestion with no maintainer
  endorsement should clear `bounded_scope`; this tension was logged in
  scan #1 and recurred unchanged with `ai-ledger#15` in scan #2.
