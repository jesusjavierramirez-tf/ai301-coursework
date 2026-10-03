# Procedure: how this tool grades a PR package

<!--
THIS IS THE PART YOU WRITE (second week running for the procedure).
Week 3 you wrote these steps for a plan package; this week the graded
object is a PR package, and the read that matters most is a
side-by-side: the diff against the plan, the evidence against the test
plan, the description against both. Your week-3 procedure is the
pattern; do not paste it unchanged, because its read order was built
for a different object.

Your rotation is the design brief again, and this week friction routes
three ways: a stall on WHAT to decide is a rubric gap, a stall on
WHERE to look is a procedure gap (this file), and a stall on what the
tool even reads or outputs is a frame gap (your SKILL.md). A complete
procedure lets someone who has never seen a PR package before grade
one exactly the way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
plan's scope pair before opening the diff, and list the files the plan
names" is a step; "understand the change" is a wish.
-->

## Read order

1. Read the issue and accepted plan context first to establish the target problem and the planned scope. This defines the expected change before you inspect the PR itself.
2. Read the plan's scope/boundary, deviation notes, and test plan. Record what was intended, what was explicitly allowed to change, and what behavior was expected after implementation.
3. Read the candidate PR title and description. Note the claims it makes about the work performed, the behavior changed, and any limitations or caveats.
4. Read the commit list and unified diff, comparing the actual change against the plan. This is the key side-by-side check: the plan, diff, and description must be compared rather than read independently because plan fidelity depends on whether the actual diff matches what was planned and what the description claims.
5. Read the test-evidence section and repo test/check results. Compare the observed results to the plan's expected-after behavior and to the reproduction steps.
6. Read the repo-facts requirements, including the PR template, contribution instructions, and stated AI-use policy. Check whether the candidate PR satisfies the repository's explicit requirements.

For live mode, use the corresponding real sources: issue/thread, plan.md and deviation notes, git diff main...HEAD, draft PR title/description, captured test output, and the repository PR template and CONTRIBUTING.md. For eval mode, use only the self-contained bundle. Never fetch outside information.

## Evidence gathering

For each rubric family, gather only the concrete evidence required for that check and record it before grading.

Plan fidelity:
- Record the planned scope/boundary and any deviation notes.
- List the meaningful changed files or implementation areas from the diff and the commit list.
- Compare the description's implementation claims against the diff and note any mismatch.
- The decision is not whether the writing is polished; it is whether the actual change stayed inside the agreed scope or was explained by a deviation note.

Test evidence:
- Record the plan's expected-after behavior.
- Record the reproduction/test steps and the evidence that was actually observed.
- Record the candidate PR test-evidence section and the repo test/check results.
- Distinguish observable evidence from unsupported statements such as "tests pass" without any visible result or check output.
- Do not require every original reproduction to be literally rerun when other evidence establishes the planned expected behavior.

Diff quality:
- Inspect the complete unified diff and the commit list.
- Identify unrelated files or hunks, debug leftovers, dead or commented-out code, and formatting churn that obscures review.
- Record the specific evidence if present so the reviewability decision is based on the repository state, not on impression.

Standards:
- Record each applicable repo requirement from the PR template, CONTRIBUTING.md, and stated policy.
- Check the candidate PR title and description for each applicable requirement and disclosure.
- Do not invent requirements that are not stated in the package.

Honesty:
- Compare claims in the PR description and test-evidence section to what the package actually establishes.
- Record disclosed limitations, missing evidence, deviations, or incomplete coverage.
- Do not treat an honestly disclosed limitation as an automatic failure if the remaining evidence still establishes readiness.

## Check execution

Execute the five rubric checks independently, in rubric order: plan_fidelity, test_evidence, diff_quality, standards, and honest. For each check:

1. Gather the evidence for that check first.
2. Grade it as pass, fail, or unclear.
3. Record one concise deciding evidence line that explains the result.

Missing or contradictory required evidence should be graded unclear rather than guessed. Do not let a strong result in one check substitute for missing evidence in another. The tool must judge the package, not the author's writing polish.

## Verdict assembly

Apply the rubric's exact verdict rule:

Accept if every required check passes.
Reject if any required check fails or is unclear.

No scoring or partial verdict. The final output must use the exact JSON structure required by CONTRACT.md, with one entry for each rubric check and a final accept/reject verdict. Do not add prose after the JSON output.
