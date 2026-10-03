# Evidence guide: where evidence lives in a PR package

<!--
THIS IS THE PART YOU WRITE (third week running: the map stays in your
hands). Your tool uses this guide as its map: for every kind of
evidence a rubric check names, this file says WHERE to find it in a PR
package and WHAT GOOD LOOKS LIKE when you do.

The four families below are the harness's failure categories under
the names the eval README uses: plan fidelity = silent-drift, test
evidence = not-tested, diff quality = unreviewable, standards and
comms = standards-wall. A package that fails none of them is a
clear-accept. Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the plan-context block's scope pair and test
  plan, the candidate PR's diff, commits, description, or
  test-evidence section, the repo-facts block's template asks and
  stated policy). In live mode (where in your working copy and on
  GitHub: your plan.md and its deviation notes, your branch's diff,
  your draft title and description, your captured test output, the
  repo's PR template and CONTRIBUTING.md).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("every changed file falls inside the
  plan's stated boundary or a deviation note") over adjectives ("the
  diff is clean").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts three ways: your
procedure says WHEN to gather each family, this guide says WHERE, and
your SKILL.md says the tool reads both. Write the map you wish your
executor had.
-->

## Plan fidelity (harness category: silent-drift)

In the eval package, look at the plan-context scope/boundary and deviation notes, the candidate PR diff, the commit list, and the description. In live mode, check plan.md and any deviation notes, the branch diff against main, the commit list, and the draft PR title/description. Good evidence compares each changed file and behavior to the plan boundary: every meaningful change sits inside the planned scope or is explicitly justified by a deviation note, and the description claims match the code that actually changed. Failure looks like silent drift: doing more than planned, omitting planned work without explanation, or describing work that the diff does not actually contain.

## Test evidence (harness category: not-tested)

In the eval package, use the plan test plan, reproduction evidence/steps, the candidate PR test-evidence section, and any repo checks or results. In live mode, use the plan test plan, reproduction steps, captured test output, and repo test/check results. Good evidence names the behavior under test, states the expected-after result, and shows an observable result proving whether it happened; this can be a direct reproduction, a focused check, or other concrete repo evidence that establishes the expected behavior. Failure looks like a vague claim such as "tests pass" without showing what was checked, what changed, or what result was observed. A literal rerun of every original reproduction is not required when other evidence clearly establishes the planned behavior.

## Diff quality (harness category: unreviewable)

In the eval package, review the unified diff and the commit list. In live mode, review git diff main...HEAD and the commit list. Good evidence shows the intended change clearly and keeps the patch focused: no unrelated edits, debug leftovers, dead code, commented-out code, or noisy formatting churn. Failure looks like a patch that is difficult to review because it contains unrelated work, stray debug statements, dead/commented code, or a broad refactor that drifts outside the plan. A focused refactor outside the plan is still relevant evidence of an unreviewable or drifted package.

## Standards and comms (harness category: standards-wall)

In the eval package, check the repo-facts PR-template requirements, CONTRIBUTING.md requirements, the stated AI-use policy, and the candidate PR title/description. In live mode, check the repository's actual PR template, CONTRIBUTING.md, the stated policy, and the draft PR title/description. Good evidence shows the required sections are filled with real content, required disclosures are present, and explicit repository requirements are addressed without inventing extra rules. Failure looks like empty boilerplate, ignored template sections, missing disclosures, or repo requirements that were not addressed. Do not invent requirements that are not stated by the repository; description fidelity belongs under plan fidelity, not standards and comms.
