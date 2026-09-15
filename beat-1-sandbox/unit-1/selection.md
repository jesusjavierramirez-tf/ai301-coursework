# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/53

**Verdict output**

#53 — PII scrubber fails to redact parenthesized US phone numbers

- repo_liveness — pass. Not archived ("archived": false); last push 2026-09-10 (4 days ago, well inside 180); last 5 default-branch commits all authored by a human (Andrew Burke, 2026-08-18 → 2026-08-24) with substantive messages; releases API returns [], i.e. no release published, which the rubric explicitly allows. docs/CONTRIBUTING.md (189 lines, 14 sections) says nothing about AI, LLM, Copilot, or generated code — policy silent, so AI-assisted work is not prohibited.
- bounded_scope — pass. One focused bug with a clear user-visible outcome: (555) 123-4567 passes through scrub() unredacted and detect() returns []. Body gives a runnable repro with observed-vs-expected output, names the file (safety/pii_scrubber.py), and names the four failing tests in tests/unit/test_pii_scrubber.py — so "done" is mechanically checkable. Author is a COLLABORATOR; labels include good first issue and tier-1. No umbrella structure, no unsettled design debate.
- no_active_claim — pass. "assignees": [], "assignee": null, "comments": 0; the timeline holds only four labeled events from the opener at creation — no cross-references, no assignment. PR search for #53 returns total_count: 0, and the repo has 0 open PRs. (Path Review's house rule would have made classmate claims non-blocking anyway; here there are none.)

Verdict: accept. All three required checks pass. On fit: this is squarely in your lane — a Python regex bug with named failing tests, which is exactly the debugging-and-testing, tightly-scoped change you said you wanted, and CONTRIBUTING's xfail contract (strict=True, remove the marker as part of the fix) gives you a second, explicit piece of the deliverable. One thing to know before you start: the four tests are currently marked @pytest.mark.xfail(strict=True), so your fix must also remove those markers or CI goes red.

{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/53",
  "checks": [
    {"name": "repo_liveness", "grade": "pass",
     "evidence": "archived=false, pushed_at 2026-09-10 (4 days before capture), last 5 main commits all by human author Andrew Burke, releases list empty (none published), docs/CONTRIBUTING.md contains no AI/LLM/generated-code restriction"},
    {"name": "bounded_scope", "grade": "pass",
     "evidence": "Single bug with repro and observed-vs-expected: \"observed: 'Call me at (555) 123-4567 or [REDACTED]'\"; names safety/pii_scrubber.py and four failing tests in tests/unit/test_pii_scrubber.py; labeled 'good first issue' and 'tier-1'; opened by a COLLABORATOR"},
    {"name": "no_active_claim", "grade": "pass",
     "evidence": "assignees: [], comments: 0, timeline shows only four 'labeled' events from the opener; PR search for #53 returns total_count 0 and the repo has 0 open PRs"}
  ],
  "verdict": "accept"
}

---

## Eval iterations

**Run history**

Run 1: 14/20  
Run 2: 18/20 (category floor not met)  
Run 3: 19/20 (category floor passed)

**Issue analysis**

`issue-12` — My rubric initially returned **accept**, while the gold label was **reject**. The issue itself looked like a focused good-first-issue, but the repository's contribution policy explicitly said that AI-generated code or documentation was not accepted. My original rubric did not check contribution policy, so it allowed the issue through. I revised `repo_liveness` to include contribution-policy eligibility.

**Check rationale**

"Pass if the repo is not archived, its last push is within 180 days of capture, the last 5 default-branch commits show human activity, and either the latest release is within 12 months of capture or the bundle says no release has been published. A published release is not required. Also pass when the policy is silent, permits AI assistance, or imposes conditions that do not prohibit the contribution; fail when the bundle explicitly prohibits AI-generated code, AI-generated documentation, or AI-generated contributions of the type required by this task."

I added the contribution-policy part to `repo_liveness` because a repository can otherwise look active and have a well-scoped issue while still being unsuitable for this course's AI-assisted workflow. The check keeps policy as an eligibility condition without rejecting repositories that simply do not mention AI.

**Trade-offs**

This policy check can reject an otherwise good issue when the repository explicitly prohibits AI-generated contributions. That is intentional because the assignment requires an AI-assisted workflow. I also kept policy silent or permissive repositories eligible so the rubric does not reject issues merely because their contribution guide does not discuss AI.

---

## Selection rationale

**Selection rationale**

1. This issue fits my interests because it is a small Python debugging task involving a regex and tests. I have worked with Python and AI/ML projects, and I want to get more experience debugging and testing an existing open-source codebase. The issue also looks small enough to work on while I am balancing the course schedule.

2. The verdict correctly identified that the issue is active, has a clear scope, has a reproducible problem, and does not have someone already working on it. What I also weighed was that the issue uses Python, names the file and tests, and gives me a good opportunity to practice working in an existing project. The rubric cannot fully measure how comfortable I will be with the codebase or how quickly I can understand its existing regex patterns.

3. I expect claiming it to be fairly straightforward because it is marked as a good first issue and currently has no assignee or open pull request. The main difficulty will probably be understanding the existing phone-number matching logic and making sure the change does not break the other supported formats.
