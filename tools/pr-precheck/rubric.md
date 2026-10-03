# Rubric: is this pull request ready to submit?

<!--
THIS IS THE PART YOU WRITE (fourth week running; this is the rubric's
final form in the sandbox). Your frame in SKILL.md executes whatever
checks you define here, via your procedure.md. It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the diff read against the plan's scope, the test
     evidence read against the plan's test plan, the description read
     against the diff, the repo-facts block's template asks) or a
     location from your references/evidence-guide.md. "The PR" is not
     a source; "the diff's changed files read against the plan's
     stated boundary" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself
     (does the diff fall inside the plan plus its deviation notes? is
     the claimed evidence observable?), never the write-up's shape
     (how long the description is, how many commits there are).
     Structure-shaped checks are what make graders disagree with
     themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (submit) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. State the `unclear`
   treatment explicitly: the frame here is YOUR SKILL.md, so a rubric
   that stays silent is only covered if your frame's grading
   discipline says what happens (the contract's own default is that
   an unverifiable claim fails).

Cover what actually gets bad PRs submitted. The failure families the
lecture named ARE the harness's scoring categories, same names as the
eval README: silent drift (the diff silently does more or less than
the posted plan, or the description claims fidelity the diff
contradicts), not tested (the evidence proves nothing observable, or
the repo's own checks were never run), unreviewable (debris or
unrelated hunks bury the change), and standards wall (the repo's
stated template and disclosure asks are ignored). Your evidence
guide's four headings map onto these one to one (plan fidelity =
silent drift, test evidence = not tested, diff quality =
unreviewable, standards and comms = standards wall), and the category
floor is scored on exactly these names plus clear accept. A rubric
that ignores a category will fail the eval packages built around
that category. And remember the honest-outcome
rule, fourth week running: a PR that honestly discloses a shortfall
can be ready; a rubric that equates "less than everything" with
"hold" fails the set.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| plan_fidelity | plan-context scope/boundary and deviation notes; candidate PR diff and commits; candidate PR description | Pass only when the meaningful changes in the diff stay within the plan's stated scope or are explained by an explicit deviation note, and the description accurately represents what the diff delivers. Both extra work beyond the plan and omitted planned work without explanation are failures. | required |
| test_evidence | plan test plan; reproduction steps/evidence; candidate PR test-evidence section; repo test/check results | Pass when the package provides observable evidence for the planned behavior, identifies the expected-after result, and shows relevant checks were actually run. A statement such as "tests pass" without observable supporting evidence is insufficient. Do not require every original reproduction to be literally rerun when other evidence establishes the planned expected behavior. | required |
| diff_quality | unified diff; commit list | Pass when the intended change is reviewable and the diff contains no unrelated changes, debug leftovers, dead code, commented-out blocks, or unrelated formatting churn that obscures review. | required |
| standards | repo-facts PR-template requirements; CONTRIBUTING.md requirements; stated AI-use policy; candidate PR title and description | Pass when all applicable repository requirements are addressed with real content, including required disclosures. Do not invent requirements that are not stated in the package. | required |
| honest | candidate PR description; test-evidence section; plan context | Pass when the PR accurately discloses relevant limitations, missing evidence, deviations, or incomplete coverage rather than claiming work or verification that the package does not establish. An honestly disclosed shortfall is not automatically a failure if the available evidence still establishes that the package is ready. | required |

## Verdict rule

Accept if every required check passes. Reject if any required check fails or is unclear.

Keep the rubric focused on the single question: "is this ready to submit?"
