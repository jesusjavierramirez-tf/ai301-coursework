# Procedure: how this skill grades a plan package

## Read order

1. Read the issue context to identify the target problem.
2. Read the repro-evidence block before reading the candidate plan so the reproduced behavior is established independently.
3. Read the repo-facts block to identify repository conventions and constraints.
4. Read the candidate plan.
5. Read the plan comment last, comparing it with the issue thread highlights and repo-facts block.

## Evidence gathering

1. Record the reproduced behavior and relevant artifacts from the repro-evidence block.
2. Record the plan's stated cause and compare it with the reproduced behavior.
3. Record the plan's in-scope, out-of-scope, files, and areas.
4. Record the implementation approach and work sequence.
5. Record the proposed tests and compare them with the reproduction steps.
6. Record stated unknowns, risks, assumptions, and deviations.
7. Record relevant thread conventions and repo contribution requirements.

## Check execution

1. Execute each rubric check against the evidence gathered for that check.
2. Mark each check pass, fail, or unclear.
3. If the required evidence is genuinely absent, mark the check unclear rather than guessing.
4. Do not use evidence from a different part of the package to silently replace missing required evidence.

## Verdict assembly

1. Apply the rubric's verdict rule to all required checks.
2. Any required fail or unclear result makes the package reject.
3. If every required check passes, accept the package.
4. Report the deciding failed or unclear check and the specific evidence supporting that result.
