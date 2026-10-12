Evidence complete. Here is the scan.

## Scan funnel

| Stage | Count | Detail |
|---|---|---|
| Queries run | 3 / 3 succeeded | 100 results each, all exit 0 |
| Combined | 300 | |
| Deduplicated by URL | **300** | zero overlap between the three queries |
| **1.** Dropped â€” has assignee | âˆ’32 | 268 remain |
| **2.** Dropped â€” bot-authored | **âˆ’99** | 169 remain |
| **3.** Sorted | 169 | `updatedAt` desc, `commentsCount` asc |
| **4.** Per-repo cap (max 2) | 0 skipped | 5 selected |

Five candidates selected, as required â€” no shortfall. Capture date **2026-10-12** (UTC, newest result in pool).

The bot filter removed 99 results across **8 distinct repos**, all `github-actions[bot]` / `type=Bot`: `mba-internship-engine` (65), `Job-Applications` (12), `fable-job-search` (7), `BigBrainTracker` (6), `ex-od-us` (4), and three others. Every one would have been graded on `is_bot`, which reads `false` for all of them.

## Ranked read-out

### âœ… Accepted (2), in fit order

**1. [stanfish06/skillquarium#1065](https://github.com/stanfish06/skillquarium/issues/1065)** â€” "[skill-suggestion] FiftyOne"
- *Query:* `"computer vision" --language Python` Â· *Signals:* rank #3 pre-cap â€” `updatedAt` 2026-10-11T13:23Z, `commentsCount=0`, no assignee, author `stanfish06` (User)
- *Fit â€” strongest of the two:* hits "computer vision" and "developer tools" in the profile directly, and the deliverable is an authored skill for a CV dataset-debugging toolkit. Maintainer-authored (`stanfish06` owns the repo), 9 stars.
- `repo_liveness` **pass** â€” not archived; pushed 2026-10-11T13:47Z; of last 5 commits, 2 are human `stanfish06` incl. "Merge pull request #1023 from stanfish06/fix/sync-quarantine"; 0 releases published; `AGENTS.md` is an operating guide *for* AI agents â€” the opposite of a ban
- `bounded_scope` **pass** â€” one focused enhancement with the gap named precisely: "the repo covers CV training/inferenceâ€¦ but has no dedicated skill for the dataset-quality/error-analysis workflow itselfâ€¦ currently only a single passing bullet inside `computer-vision-scientist/SKILL.md`". Labelled `skill-suggestion`; 2,100+ existing skills supply the target structure
- `no_active_claim` **pass** â€” `assignees: []`, `closedByPullRequestsReferences: []`, `comments: []`

**2. [PythonMuse/ai-ledger#15](https://github.com/PythonMuse/ai-ledger/issues/15)** â€” "Supervised and Unsupervised Machine Learning"
- *Query:* `"machine learning" --language Python` Â· *Signals:* rank #1 â€” newest `updatedAt` in pool (2026-10-12T03:44Z), `commentsCount=0`, no assignee, author `patricktoohey` (User)
- *Fit â€” weaker:* AI/ML subject matter, but the deliverable is prose, not code, in a 1-star repo
- `repo_liveness` **pass** â€” not archived; pushed 2026-10-11T22:29Z; all 5 last commits authored by human `PythonMuse`; 0 releases; `CONTRIBUTING.md` silent on AI
- `bounded_scope` **pass** â€” one documentation task naming a section: "Classify Each Step discusses pattern detection and maybe it would be useful to note the distinction between Supervised and Unsupervised ML"
- `no_active_claim` **pass** â€” no assignee, no linked PR, no comments

> Same rubric tension as scan #1, logged not overridden: "*maybe* it would be useful" is a hedge, and no maintainer has responded. The rubric says maintainer authorship isn't required, so it passes as written.

### âŒ Rejected (3)

**3. [coinbase/cdp-sdk#848](https://github.com/coinbase/cdp-sdk/issues/848)** â€” x402 discovery API silently ignores filters
- *Query:* `"API bug"` Â· *Signals:* rank #2 â€” `updatedAt` 2026-10-12T01:12Z, `commentsCount=2`
- **Sunk by `bounded_scope`** â€” "Please move or close it if there is a better venue, and tell me where." The fix lives in a hosted API, not this repo; three fixes offered "in order of preference"; the thread widens scope to all filters. No maintainer has settled any of it.
- `repo_liveness` **pass** â€” pushed 2026-10-06; commits are `cdp-repo-sync[bot]` but PR #841 was merged by human `sammccord`, which the evidence guide counts as maintainer life. `no_active_claim` **pass** â€” both commenters are `authorAssociation: NONE` reproductions, neither claims the work.

**4. [virtual-labs/bugs-virtual-labs#20241](https://github.com/virtual-labs/bugs-virtual-labs/issues/20241)** â€” "[BUG REPORT] Basic machine learning using the WEKA tool"
- *Query:* `"machine learning"` Â· *Signals:* rank #4 â€” `updatedAt` 2026-10-11T07:33Z, `commentsCount=0`, author `vlabs-bug` (**User** type â€” survived the bot filter)
- **Sunk by `repo_liveness`** â€” all 5 default-branch commits are `vlabs-bug` / "Adding an image to the repository": a bug-intake account uploading form attachments, not human development
- **Also sunk by `bounded_scope`** â€” an auto-generated web-form report whose entire content is "Type(s) of Issue - Page Not Loading" plus "Additional info- Experimental" and a machine-readable JSON blob. The failing page is a hosted site (`bcb-au.vlabs.ac.in`) and this repo is a tracker, not that site's code. Finding what to even change is investigation, not a defined deliverable.
- `no_active_claim` **pass** â€” no assignee, no linked PR, no comments
- *(The body embeds a reporter's personal email address; not quoting it.)*

**5. [aws-samples/sample-agentcore-cloudfront-x402-payments#39](https://github.com/aws-samples/sample-agentcore-cloudfront-x402-payments/issues/39)** â€” "Add Bug Bounty Intelligence as x402 merchant example"
- *Query:* `"API bug"` Â· *Signals:* rank #5 â€” `updatedAt` 2026-10-11T04:23Z, `commentsCount=1` (stale â€” see friction)
- **Sunk by `bounded_scope`** â€” a third party proposing their own commercial paid endpoint (5 USDC/scan, their own domain) for listing, closing with "Happy to adjust format/fields to match how the other examples are listed." Whether to list a vendor at all is an unresolved product decision only a maintainer can make, and none has: open since 2026-07-26 with **zero comments in 2.5 months**, in a repo whose last code commit (2026-05-12) predates the issue.
- `repo_liveness` **pass** â€” not archived; pushed 2026-06-29 (105 days, within 180); last 5 commits by human "Joshua Smith" incl. `joshuamarksmith` merging PR #21; 0 releases; `CONTRIBUTING.md` present with no AI mentions. `no_active_claim` **pass** â€” verified 0 comments directly via the comments API.

```json
[
  {
    "item": "https://github.com/stanfish06/skillquarium/issues/1065",
    "checks": [
      {"name": "repo_liveness", "grade": "pass", "evidence": "Not archived; pushed 2026-10-11T13:47:05Z; 2 of last 5 commits by human stanfish06 incl. 'Merge pull request #1023 from stanfish06/fix/sync-quarantine'; 0 releases published; AGENTS.md is an operating guide for AI agents, not a ban."},
      {"name": "bounded_scope", "grade": "pass", "evidence": "One focused enhancement, gap named by the repo owner: 'no dedicated skill for the dataset-quality/error-analysis workflow itself... currently only a single passing bullet inside computer-vision-scientist/SKILL.md'; labelled skill-suggestion."},
      {"name": "no_active_claim", "grade": "pass", "evidence": "assignees: [], closedByPullRequestsReferences: [], comments: []."}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/PythonMuse/ai-ledger/issues/15",
    "checks": [
      {"name": "repo_liveness", "grade": "pass", "evidence": "Not archived; pushed 2026-10-11T22:29:36Z; all 5 last default-branch commits authored by human 'PythonMuse'; 0 releases published; CONTRIBUTING.md silent on AI."},
      {"name": "bounded_scope", "grade": "pass", "evidence": "One documentation task naming a specific section: 'Classify Each Step discusses pattern detection and maybe it would be useful to note the distinction between Supervised and Unsupervised ML'."},
      {"name": "no_active_claim", "grade": "pass", "evidence": "assignees: [], closedByPullRequestsReferences: [], comments: []."}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/coinbase/cdp-sdk/issues/848",
    "checks": [
      {"name": "repo_liveness", "grade": "pass", "evidence": "Not archived; pushed 2026-10-06T16:41:48Z; sync PR #841 merged by human 'sammccord'; 0 releases; CONTRIBUTING.md silent on AI."},
      {"name": "bounded_scope", "grade": "fail", "evidence": "Body states 'Please move or close it if there is a better venue, and tell me where' â€” fix lives in a hosted API, three preference-ordered fixes offered, thread widens scope to all filters, none settled by a maintainer."},
      {"name": "no_active_claim", "grade": "pass", "evidence": "assignees: [], no linked PRs; both comments are authorAssociation NONE reproductions, neither claims the work."}
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/virtual-labs/bugs-virtual-labs/issues/20241",
    "checks": [
      {"name": "repo_liveness", "grade": "fail", "evidence": "All 5 default-branch commits are account 'vlabs-bug' with message 'Adding an image to the repository' â€” bug-intake attachment uploads, not human development activity."},
      {"name": "bounded_scope", "grade": "fail", "evidence": "Auto-generated web-form report whose content is 'Type(s) of Issue - Page Not Loading' plus 'Additional info- Experimental'; failing page is a hosted site (bcb-au.vlabs.ac.in) and this repo is a tracker, not that site's code."},
      {"name": "no_active_claim", "grade": "pass", "evidence": "assignees: [], closedByPullRequestsReferences: [], comments: []."}
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/aws-samples/sample-agentcore-cloudfront-x402-payments/issues/39",
    "checks": [
      {"name": "repo_liveness", "grade": "pass", "evidence": "Not archived; pushed 2026-06-29T04:21:32Z (105 days, within 180); last 5 commits by human 'Joshua Smith' incl. joshuamarksmith merging PR #21; 0 releases; CONTRIBUTING.md has no AI mentions."},
      {"name": "bounded_scope", "grade": "fail", "evidence": "Third party proposing their own paid endpoint (5 USDC per scan) for listing, asking 'Happy to adjust format/fields to match how the other examples are listed'; unresolved maintainer product decision, open since 2026-07-26 with zero comments."},
      {"name": "no_active_claim", "grade": "pass", "evidence": "assignees: [], no linked PRs; comments API returns count=0."}
    ],
    "verdict": "reject"
  }
]
```

## Friction

Not patching anything, per your instruction â€” recording only.

**The bot filter worked, and bigger than expected.** It removed 99 of 268 (37%), and critically it was *not* a one-repo problem: eight separate repos were flooding the pool with `github-actions[bot]` issues. Scan #1's diagnosis undercounted this. Yield went from 1/5 to **2/5**, and both accepts are defensible.

**The per-repo cap never engaged â€” 0 skips.** It's untested by this scan. The bot filter removed the flood upstream, so the cap had nothing to catch. It remains a reasonable backstop for a human-authored flood, but don't read this run as validating it.

**New gap: automation accounts that aren't typed as `Bot`.** `vlabs-bug` is a plain User account that files auto-generated form reports and makes mechanical commits. Neither `author.type == "Bot"` nor the `[bot]` suffix catches it, so it consumed a grading slot and then failed two rubric checks. The bot filter catches GitHub Apps, not role accounts.

**Search `commentsCount` is stale.** Candidate #5 was returned with `commentsCount=1`; the comments API returns 0. It's a tie-breaker input, so a stale value can misorder results â€” here it changed nothing, since `updatedAt` was unique.

**Recurring rubric gaps, both of which bit again:**
- *Wrong venue* â€” two of five (#3 an API bug in an SDK repo, #4 a hosted-site bug in a tracker repo). Still no dedicated check.
- *No maintainer-engagement floor* â€” `repo_liveness` passed both extremes: an issue hours old with no reply, and one sitting 2.5 months with zero reply in a repo whose last commit predates it.
- *"Human activity" threshold undefined* â€” skillquarium passed on 2 of 5 human commits, virtual-labs failed on 0 of 5. The rubric never says how many of the five must be human, so I was interpreting rather than applying.

**Tooling:** the `\` line continuations in the repaired strategy are POSIX-only; I joined each command onto one line for PowerShell, as flagged before running. Everything else behaved.
